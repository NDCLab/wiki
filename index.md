---
layout: default
title: Home
nav_order: 1
---

# Neural Dynamics of Control (NDC) Lab Wiki

<img src="ndcwikiicon.png"
     alt="NDC Wiki Icon"
     width="80"
     height="80"/> Welcome to the Neural Dynamics of Control (NDC) Lab Wiki.

This wiki is the main source of documentation for researchers and developers contributing to the lab. For further information about the NDC Lab, please visit our [external website](http://www.ndclab.com/).


<!-- [Get started now](#getting-started){: .btn .btn-primary .fs-5 .mb-4 .mb-md-0 .mr-2 }  -->
[View on GitHub](https://github.com/NDCLab/wiki){: .btn .btn-primary .fs-5 .mb-4 .mb-md-0 .mr-2 }
[Return to Main](https://ndclab.github.io/){: .btn .fs-5 .mb-4 .mb-md-0 }

### Our Contributors
<ul class="list-style-none">
{% for contributor in site.github.contributors %}
  <li class="d-inline-block mr-1">
     <a href="{{ contributor.html_url }}"><img src="{{ contributor.avatar_url }}" width="32" height="32" alt="{{ contributor.login }}"/></a>
  </li>
{% endfor %}
</ul>
