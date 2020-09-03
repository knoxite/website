+++
fragment = "content"
#disabled = true
date = "2020-04-10"
weight = 80
background = "dark"

title = "Store your data wherever you want"
subtitle = "Not only can you connect Knoxite to a wide range of Cloud services, you can even combine them all and make the most of your available space."
title_align = "left" # Default is center, can be left, right or center

[sidebar]
  align = "right"
  sticky = true # Default is false
  content = """
<center>

  <span style="font-size: 64px;">
    <i class="fas fa-desktop fa-fw" style="color:lightgrey;"></i>
  </span>
  <span style="font-size: 64px;">
    <i class="fas fa-network-wired fa-fw" style="color:lightgrey;"></i>
  </span>
  <span style="font-size: 64px;">
    <i class="fab fa-aws fa-fw" style="color:lightgrey;"></i>
  </span>
  <span style="font-size: 64px;">
    <i class="fab fa-dropbox fa-fw" style="color:lightgrey;"></i>
  </span>
  <span style="font-size: 64px;">
    <i class="fas fa-cloud-upload-alt fa-fw" style="color:lightgrey;"></i>
  </span>

</center>
"""
+++

<p>You've chosen a cloud provider for your data before? We may already support it!</p>
<p>Select between various protocols and standards like SSH, WebDAV or FTP or cloud providers like Google Drive, NextCloud, DropBox and many others!</p>

[<button class="btn btn-success mt-4">See all storage backends</button>](/docs/storage-backends)
