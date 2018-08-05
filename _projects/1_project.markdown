---
layout: page
title: BioMEMS
description: Microbubble length tracking using image processing
img: /assets/img/BioMEMS_project/bubble_crop1.gif
---

***

<p>
  <img src="/assets/img/BioMEMS_project/bubble.gif" style="width: 70%;"/>
</p>

## Introducing a pressure sensor

I spent two years in USC Biomedical Microsystems Laboratory working as an undergraduate researcher. One of the projects aims to treat hydrocephalus via a novel pressure sensor.[^note1] Hydrocephalus occurs when excessive cerebrospinal fluid accumulates in the brain, resulting in an abnormal widening of spaces. Since fluid accumulation poses potentially life-threatening pressure against brain tissues, it is necessary to monitor pressure chronically to drive timely therapeutic interventions. Hence, a new, flexible, MEMS-based, low-powered, biocompatible pressure sensor was being developed. This pressure sensor enables reliable sensing for chronic *in-vivo* implantation and provides immediate access to actionable pressure data. My job is to characterize the transducer's design to maximize its sensitivity. So how does it work?


## Principle of pressure sensing using a microbubble

The key idea of the design exploits how microbubbles respond instantaneously to external pressure variations. By isolating the microbubble in a microchannel filled with an electrolyte solution, we are able to mimic the wet, *in-vivo* environment of cerebrospinal fluid in hydrocephalus. Our goal is to infer pressure change by monitoring the behavior of the bubble dissolution.

> **Boyle's law** tells us that pressure of a gas is inversely related to its volume ($$ P \varpropto \frac{1}{V} $$).
> **Henry's law** tells us bubble dissolution rate linearly corresponds to change in pressure.


A microchannel is carefully fabricated into the device. The channel is connected with four electrodes: two on each side to measure the electrochemical differences (e.g. impedance) and two in the middle to generate a microbubble.

<p>
  <img src="/assets/img/BioMEMS_project/deviceFFC.png" style="width: 28%;"/>
  <img src="/assets/img/BioMEMS_project/device.jpg" style="width: 33%;"/>
  <img src="/assets/img/BioMEMS_project/devicechannel.png" style="width: 34%;"/>
</p>
<p>
<div class="caption">
    The design of a pressure transducer: left: A MEMS device connected with a FFC cable; middle: a zoomed image of the microbubble pressure transducer (μBPT); right: a further magnified image of pressure part of the μBPT, with and without a bubble injection in the microchannel.
</div>
</p>

We first completely fill the microchannel with phosphate buffered saline (PBS) to mimic a wet, *in-vivo* environment. By a current-induced electrolysis from the nuclear cores, we create a microbubble from the middle of the channel.

<p>
    <img src="/assets/img/BioMEMS_project/cross_section.png" style="float: right; width:35%;"/>
</p>
When a microbubble is trapped within a filled chamber with rectangular cross section, the gas tends to fill the middle of the cross sectional area and leave pockets of liquid at the corners. These capillaries allow an ionic conduction path within the channel.[^law]

One electrochemical characterization we do is to chronically measure changes in impedance conducted through the liquid capillaries at the corners.[^law] Though it is a good indicator of pressure change, a big obstacle we discover is the instability in impedance measurement from the microbubble generation. So we explore alternative ways to characterize microbubble behavior other than the established method of measuring impedance.

## Bubble length tracking

In response to a pressure change, bubble length is more likely to vary than the cross section area in a microchannel.[^footnote1] So can we infer pressure through tracking microbubble length, rather than using impedance measurements? With some simple image processing on the bubble snapshots taken 2 frames per second, we implement a Matlab program that automatically tracks changes of the microbubble volume in response to pressure.

We take the raw, cropped, straightened image of the microchannel and subtract it from the initial image taken before a bubble is injected. By processing it into a B/W image of the isolated bubble, we then implement a program to track both ends of the bubble. Note that the markers on top of the channel are 100µm apart. They provide us a nice basis to measure the actual bubble length.

<p class="aligncenter">
<img src="/assets/img/BioMEMS_project/bubblelength.png" style="width: 80%;vertical-align: middle;"/>
    <div class="caption">
    Top to bottom: raw image of the microchannel, processed B/W image of the bubble, and a snapshot of how the program tracks the bubble's length, respectively.
    </div>
</p>

If you're interested in the actual code, click open the collapsible:
<details>
    <summary>Matlab Code</summary>

    {% highlight matlab %}
    % iternate for the whole set of images
    files = dir(fullfile(mydir, 'img*.jpg'));
    first = 'img.jpg';
    count = 0;
    for file = files'
        fname = file.name;
        disp(fname);
        count = count + 1;
    % only start processing after the first image (the 'base' image)
        if (strcmp(fname,first))
            base = imread(fullfile(mydir, fname),'jpg');
            base = rgb2gray(base);
            basecropped = imcrop(base,crop_parameter);
            basecropped = imrotate(basecropped,angle,'bilinear','crop');
        else
            im = imread(fullfile(mydir, fname),'jpg');
            im = rgb2gray(im);
            imcropped = imcrop(im,crop_parameter);
            imcropped = imrotate(imcropped,angle,'bilinear','crop');
    % Subtract from the initial 'base' image that has no bubble
            diff = (imcropped - basecropped);
            diff = imadjust(diff);
    % ensure we get the correct length by measuring multiple rows
            for i = 0:2:test_rows
                [row,col] = find(diff(i+starting_row,:) > cut_off_pixel);
                [row5,col5] = find(diff(i+starting_row+5,:) > cut_off_pixel);
                [row10,col10] = find(diff(i+starting_row+10,:) > cut_off_pixel);
                [row15,col15] = find(diff(i+starting_row+15,:) > cut_off_pixel);
                combcol = union(col,col5);
                combcol = union(combcol,col10);
                combcol = union(combcol,col15);
                if(isempty(combcol))
                    bubble_length_ratio = [bubble_length_ratio;0];
                else
                    bubble_length = combcol(end)-combcol(1);
    % sometimes the the image is fuzzy or not cropped properly
                    continuous = bubble_length/(size(combcol,2)-size(combcol,1));
                    if(continuous < 1.5)
                        bubble_length_ratio = [bubble_length_ratio;bubble_length/base_length];
                    else
                        bubble_length_ratio = [bubble_length_ratio;0];
                    end
                end
            end
            bubble_length_array = [bubble_length_array, bubble_length_ratio];
            [max_ratio,max_row] = max(bubble_length_ratio);
            max_ratio
            max_row = starting_row + max_row;
            max_ratio_array = [max_ratio_array, max_ratio];
    %displaying images
            [row,col] = find(diff(max_row,:) > cut_off_pixel);
            [row5,col5] = find(diff(max_row+5,:) > cut_off_pixel);
            [row10,col10] = find(diff(max_row+10,:) > cut_off_pixel);
            [row15,col15] = find(diff(max_row+15,:) > cut_off_pixel);
            if(disp_images && count-1>=starting_image && count-1<=ending_image)
                figure
                imshow(diff);
                title(num2str(fname));
                hold on;
                if(~isempty(col))
                    plot(col,max_row,'rx', 'MarkerSize', 5);
                end
                if(~isempty(col5))
                    plot(col5,max_row+5,'bx', 'MarkerSize', 5);
                end
                if(~isempty(col10))
                    plot(col10,max_row+10,'gx', 'MarkerSize', 5);
                end
                if(~isempty(col15))
                    plot(col15,max_row+15,'yx', 'MarkerSize', 5);
                end
                pause(.2);
            end
            bubble_length_ratio = [];
        end
    end
    {% endhighlight %}
</details>


## Results

<p>
    <img src="/assets/img/BioMEMS_project/length_pressure.png" style="width: 49%;"/>
    <img src="/assets/img/BioMEMS_project/length_time.png" style="width: 49%;"/>
    <div class="caption">
    Left: the maximum lengths of the microbubble at different pressure setting. Right: the change in microbubble length over time, from its injection till dissolution at different pressure setting.
    </div>
</p>

If we compare the bubble length results to the impedance measurements[^note2], we can see some similarities. Both bubble length and impedance measurements show us their inverse relationships with pressure, and can capture the essence of the microbubble behavior inside the channel in a similar fashion.

<p>
  <img src="/assets/img/BioMEMS_project/impedance_pressure.png" style="width: 49%;"/>
  <img src="/assets/img/BioMEMS_project/impedance_time.png" style="width: 49%;"/>
    <div class="caption">
    Left: the change in impedance magnitude (∆Z) due to the bubble injection at different pressure setting. Right: the change in impedance over time, from its injection till dissolution at different pressure setting.
    </div>
</p>

We have shown microbubble length tracking is a nice and intuitive visual tool for us to monitor bubble dissolution. However, there is one issue remains unsolved - we couldn't quite explain the correlations between the two indicators (bubble length and impedance). If we plot the two measurements overlapping each other, as the bubble dissolves, the two measurements appear to have different curves as the bubble dissolves.[^note3]

<p>
  <img src="/assets/img/BioMEMS_project/compare.png" style="width: 100%;"/>
    <div class="caption">
    Of all 10 bubble injection experiments on one device, both bubble length and impedance measurements demonstrate a sharp raise when the bubble is injected and occupies a maximum volume in the channel, and a graduate drop when the bubble slowly dissolves into the solution. Yet, the curves do not exactly align with one another. But, does it matter?
    </div>
</p>

## Conclusion

Impedance measurements remain to be a precise benchmark for our device characterization, but this project provides us an alternative visual indicator of the device performance. It can be especially useful when the electrochemical performance is unstable/unreliable for some devices.

***

[^note1]: It is worth mentioning that this pressure sensor can also be applicable to other common pressure-induced medical conditions, such as hypertension and glaucoma.

[^law]: L. Yu, C. A. Gutierrez, E. Meng. An Electrochemical Microbubble-based MEMS Pressure Sensor. Journal of Microelectromechanical Systems. Vol 25. 2016.

[^footnote1]: S. Ma, et al: Effect of Contact Angle on Drainage and Imbibition in Regular Polygonal Tubes. Colloid Surf. A. 117. 1996.

[^note2]: The impedance measurements are actually from another device. The resulted images are from [^law]. Even so, because the underlying principle is unchanged, this comparison is still valid to show an overall idea.

[^note3]: In this plot we obtain both impedance measurements and the snapshot images at the same time, meaning the overlapping graph presents results of the same set of experiments of the same device.
