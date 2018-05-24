# Pose Guided Person Image Generation
<script type="text/javascript" src="http://cdn.mathjax.org/mathjax/latest/MathJax.js?config=default"></script>
**Architecture**
![PGPIG_Architecture](https://raw.githubusercontent.com/bj80heyue/CVPR2018_PaperReading/master/img/PGPIG_0.png)

**Contribution**

* A novel task of conditioning image generation on a
reference image and an intended pose
* A novel mask loss is proposed to encourage the model to focus on transferring the human body appearance instead of background information
* Two stage: *stage-I* focusing on global structure of the human body; the *stage-II* on filling in appearance details based on the first stage result

**Details**

1. Encode key points as 18 heatmaps. Each heatmap is filled with 1 in a radius of 4 pixels around the corresponding keypoints and 0 elsewhere.

	`· If use gaussian process rather than binary.Maybe it will perform better?`
	`· Why not use skeleton as heatmap?`

2. Pose mask loss : set to 1 for foreground and 0 for background, finally mask = (1+Mp).
![PGPIG_PoseMaskLoss](https://raw.githubusercontent.com/bj80heyue/CVPR2018_PaperReading/master/img/PGPIG_1.png)

	`Maybe soft boundary is better?`
	
3. In stage-II,the fully-connected layer is removed from the U-Net. This helps to preserve more details from the input because a fully-connected layer compresses a lot of information contained in the input.

4. The pairwise input encourages D to learn the distinction between syn-image and gt-image instead of only the distinction between synthesized and natural images(reference).

**Result**
![PGPIG_Result](https://raw.githubusercontent.com/bj80heyue/CVPR2018_PaperReading/master/img/PGPIG_2.png)


