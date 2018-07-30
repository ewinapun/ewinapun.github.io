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

The key idea behind the design exploits how microbubbles respond instantaneously to external pressure variations. By isolating the microbubble in a microchannel filled with an electrolyte solution, we are able to mimic the wet, *in-vivo* environment of cerebrospinal fluid in hydrocephalus. Our goal is to infer pressure change by monitoring the behavior of the bubble dissolution.

> **Boyle's law** tells us that pressure of a gas is inversely related to its volume ($$ P \varpropto \frac{1}{V} $$).
> **Henry's law** tells us bubble dissolution rate linearly corresponds to change in pressure.


A microchannel is carefully fabricated into the device. The channel is connected with four electrodes: two on each side to measure the electrochemical differences (e.g. impedance) and two in the middle to generate a microbubble.

<p>
  <img src="/assets/img/BioMEMS_project/deviceFFC.png" style="width: 28%;"/>
  <img src="/assets/img/BioMEMS_project/device.jpg" style="width: 35%;"/>
  <img src="/assets/img/BioMEMS_project/devicechannel.png" style="width: 35%;"/>
</p>
<div class="caption">
    The design of a pressure transducer: left: A MEMS device connected with a FFC cable; middle: a zoomed image of the microbubble pressure transducer (μBPT); right: a further magnified image of pressure part of the μBPT, with and without a bubble injection in the microchannel.
</div>


We first completely fill the microchannel with phosphate buffered saline (PBS) to mimic a wet, *in-vivo* environment. By a current-induced electrolysis from the nuclear cores, we create a microbubble from the middle of the channel.

<p>
    <img src="/assets/img/BioMEMS_project/cross_section.png" style="float: right; width:35%;"/>
</p>
When a microbubble is trapped within a filled chamber with rectangular cross section, the gas tends to fill the middle of the cross sectional area and leave pockets of liquid at the corners. These capillaries allow an ionic conduction path within the channel.[^law]

One electrochemical characterization we do is to chronically measure changes in impedance conducted through the liquid capillaries at the corners.[^law] Though it is a good indicator of pressure change, a big obstacle we discover is the instability in impedance measurement from the microbubble generation. So we explore alternative ways to characterize microbubble behavior other than the established method of measuring impedance.

## Bubble length tracking

In response to a pressure change, bubble length is more likely to vary than the cross section area in a microchannel.[^footnote1] So can we track the bubble length on top of the impedance measurement? With some simple image processing on the snapshots taken 2 frames per second, we implement a Matlab program that automatically tracks changes of the microbubble volume in response to pressure.

<details><summary>Matlab Code</summary>
<p>

```python
% iternate for the whole set of images
files = dir(fullfile(mydir, 'img*.jpg'));
first = 'img.jpg';
for file = files'
    fname = file.name;
    count = count + 1;
    if (strcmp(fname,first))
        base = imread(fullfile(mydir, fname),'jpg'); base = rgb2gray(base);
        basecropped = imcrop(base,crop_parameter);
        basecropped = imrotate(basecropped,angle,'bilinear','crop');
    else
        im = imread(fullfile(mydir, fname),'jpg'); im = rgb2gray(im);
        imcropped = imcrop(im,crop_parameter);
        imcropped = imrotate(imcropped,angle,'bilinear','crop');
        % Subtract from another photo
        diff = (imcropped - basecropped);
        diff = imadjust(diff);

        for i = 0:2:test_rows
            [row,col] = find(diff(i+starting_row,:) > cut_off_pixel);
            [row5,col5] = find(diff(i+starting_row+5,:) > cut_off_pixel);
            [row10,col10] = find(diff(i+starting_row+10,:) > cut_off_pixel);
            [row15,col15] = find(diff(i+starting_row+15,:) > cut_off_pixel);
            combcol = union(col,col5); combcol = union(combcol,col10);
            combcol = union(combcol,col15);
            if(isempty(combcol))
                bubble_length_ratio = [bubble_length_ratio;0];
            else
                bubble_length = combcol(end)-combcol(1);

                % check if it's a fuzzy image or an actual channel
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
        [row,col] = find(diff(max_row,:) > cut_off_pixel);
        [row5,col5] = find(diff(max_row+5,:) > cut_off_pixel);
        [row10,col10] = find(diff(max_row+10,:) > cut_off_pixel);
        [row15,col15] = find(diff(max_row+15,:) > cut_off_pixel);

        %displaying images
        if(disp_images && count-1>=starting_image && count-1<=ending_image)
            diff_copy = diff;
%             figure
%             title(num2str(fname));
%             imshow(basecropped);
            figure
            imshow(diff_copy);
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
        % each for loop return to zero
        bubble_length_ratio = [];
    end
end
```

</p>
</details>

<p>
  <img src="/assets/img/BioMEMS_project/bubblelength.png" style="width: 90%;"/>
</p>
<div class="caption">
Nothing very fancy in fact: We took the raw, cropped, straightened image of the microchannel and subtract it from the first image taken before a bubble is injected. By processed into a B/W image of the bubble isolated;bottom: screenshot of how we track the bubble's length.
</div>


So this is what I got:

<p>
  <img src="/assets/img/BioMEMS_project/length_pressure.png" style="width: 49%;"/>
  <img src="/assets/img/BioMEMS_project/length_time.png" style="width: 49%;"/>
</p>

<div class="caption">
Top: raw, cropped image of the microchannel; middle: processed B/W image of the bubble; bottom: screenshot of the program that tracks the bubble's length.
</div>

The results are actually comparable to that using impedance measurements. This is as expected, but this project provides a very useful visual indicator of the device performance, especially when impedance measurements

<p>
  <img src="/assets/img/BioMEMS_project/impedance_pressure.png" style="width: 49%;"/>
  <img src="/assets/img/BioMEMS_project/impedance_time.png" style="width: 49%;"/>
</p>
<div class="caption">
Top: raw, cropped image of the microchannel; middle: processed B/W image of the bubble; bottom: screenshot of the program that tracks the bubble's length.
</div>

***

[^note1]: It is worth mentioning that this pressure sensor can also be applicable to other common pressure-induced medical conditions, such as hypertension and glaucoma.

[^law]: L. Yu, C. A. Gutierrez, E. Meng. An Electrochemical Microbubble-based MEMS Pressure Sensor. Journal of Microelectromechanical Systems. Vol 25. 2016.

[^footnote1]: S. Ma, et al: Effect of Contact Angle on Drainage and Imbibition in Regular Polygonal Tubes. Colloid Surf. A. 117. 1996.

