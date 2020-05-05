+++
fragment = "content"
weight = 100
#background = ""
#categories = ["knoxite", "blog"]

title = "This week in knoxite - Week 16 to 18/2020"
title_align = "left"
summary = "Read what happened in the weeks 16 to 18 in this blogpost."

display_date = true
date = "2020-04-21"
+++

A warm welcome from your knoxite team in this blogpost reporting about the 
progress we did in the weeks 16 to 18 of 2020.

As last week, we will start off with the...

## development side of knoxite!


On the development side of things, a lot of refectoring work was done by muesli.
The repository now follows the convention, that the 
[binaries should be separated from the code.](https://medium.com/@benbjohnson/structuring-applications-in-go-3b04be4ff091#0745)
Note that this also changes the way you have to compile knoxite. If you want
to know more, check out our 
[README.md](https://github.com/knoxite/knoxite/blob/master/README.md)
or the
[installation guide](https://knoxite.com/docs/installation/#download-knoxite).

As new features we have a new backend serving the google cloud storage thanks
to @mahartma.

We are also currently working on tests. The WebDav-tests are already finshed by
CraftAMap, while the Azure- and Google-Cloud-Tests are done by mahartma, and
should be done the next days. penguwin is working on the mega.nz tests.
Thanks to the big effort of @muesli, we also switched from `Travis CI` to 
`GitHub Actions`.

Thanks to craftamap, we also fixed a bug with the `repo add` command.

## On the "meta"-side of things...

We did a lot of small changes on our website and our documentation.
On the website, we added a lightbox for our images (thanks to @craftamap).

Thanks to the whole team (huge shoutout to @penguwin) for updating the 
documentation as well as the "getting started"-guide.

If you want to get the latest news of our development "live", you can also join
our IRC-Channel, where you can read the events happening on our repositories. 
Thanks @penguwin for creating the `knoxitebee`, a 
[beehive bee](https://github.com/muesli/beehive).


Thats it for the last weeks! Stay tuned for the next blogpost!
