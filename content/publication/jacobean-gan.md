+++
title = "Is Generator Conditioning Causally Related to GAN Performance?"
date = 2018-07-12T12:27:43Z
draft = false

# Authors. Comma separated list, e.g. `["Bob Smith", "David Jones"]`.
authors = ["Augustus Odena", "Jacob Buckman", "Catherine Olsson", "Tom B. Brown", "Christopher Olah", "Colin Raffel", "Ian Goodfellow"]

# Publication type.
# Legend:
# 0 = Uncategorized
# 1 = Conference paper
# 2 = Journal article
# 3 = Manuscript
# 4 = Report
# 5 = Book
# 6 = Book section
publication_types = ["1"]

# Publication name and optional abbreviated version.
publication = "Is Generator Conditioning Causally Related to GAN Performance?"
publication_short = ""

# Abstract and optional shortened version.
abstract = "Recent work (Pennington et al, 2017) suggests that controlling the entire distribution of Jacobian singular values is an important design consideration in deep learning. Motivated by this, we study the distribution of singular values of the Jacobian of the generator in Generative Adversarial Networks (GANs). We find that this Jacobian generally becomes ill-conditioned at the beginning of training. Moreover, we find that the average (with z from p(z)) conditioning of the generator is highly predictive of two other ad-hoc metrics for measuring the 'quality' of trained GANs: the Inception Score and the Frechet Inception Distance (FID). We test the hypothesis that this relationship is causal by proposing a 'regularization' technique (called Jacobian Clamping) that softly penalizes the condition number of the generator Jacobian. Jacobian Clamping improves the mean Inception Score and the mean FID for GANs trained on several datasets. It also greatly reduces inter-run variance of the aforementioned scores, addressing (at least partially) one of the main criticisms of GANs."
abstract_short = "We study the distribution of singular values of the Jacobian of the generator in Generative Adversarial Networks (GANs), and find that the average conditioning of the generator is highly predictive of other metrics for measuring the 'quality' of trained GANs.
We test the hypothesis that this relationship is causal by proposing a 'regularization' technique (called Jacobian Clamping) that softly penalizes the condition number of the generator Jacobian.

# Featured image thumbnail (optional)
image_preview = ""

# Is this a selected publication? (true/false)
selected = false

# Projects (optional).
#   Associate this publication with one or more of your projects.
#   Simply enter the filename (excluding '.md') of your project file in `content/project/`.
#   E.g. `projects = ["deep-learning"]` references `content/project/deep-learning.md`.
projects = []

# Tags (optional).
#   Set `tags = []` for no tags, or use the form `tags = ["A Tag", "Another Tag"]` for one or more tags.
tags = []

# Links (optional).
url_pdf = ""
url_preprint = "https://arxiv.org/abs/1802.08768"
url_code = ""
url_dataset = ""
url_project = ""
url_slides = ""
url_video = ""
url_poster = ""
url_source = ""

# Custom links (optional).
#   Uncomment line below to enable. For multiple links, use the form `[{...}, {...}, {...}]`.
# url_custom = [{name = "Custom Link", url = "http://example.org"}]

# Does this page contain LaTeX math? (true/false)
math = false

# Does this page require source code highlighting? (true/false)
highlight = true

# Featured image
# Place your image in the `static/img/` folder and reference its filename below, e.g. `image = "example.jpg"`.
[header]
image = ""
caption = ""

+++
