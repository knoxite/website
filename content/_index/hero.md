+++
fragment = "hero-terminal"
#disabled = true
date = "2020-04-20"
weight = 50
background = "dark" # can influence the text color
particles = false

subtitle = "An open-source data storage & backup system"

[header]
  image = "header.jpg"

[asset]
  image = "knoxite-logo.png"
  #width = "500px" # optional - will default to image width
  #height = "150px" # optional - will default to image height

[terminal]
  src = "/casts/tutorial.cast"
  class = "rounded d-none d-sm-none d-md-none d-lg-block"
  #theme = "monokai" #theme is optional, if nothing is set we use monokai
  #autoplay = "false" # is true by default
  #loop = "loop" # is look by default
  rows = "20" #
  #columns = "" #

[[buttons]]
  text = "Download"
  url = "/docs/installation"
  color = "primary"

[[buttons]]
  text = "Get Started"
  url = "/docs/getting-started"
  color = "primary"

[[buttons]]
  text = "Docs"
  url = "/docs"
  color = "primary" # primary, secondary, success, danger, warning, info, light, dark, link - default: primary

+++
