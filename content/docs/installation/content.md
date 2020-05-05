+++
fragment = "content"
weight = 100
title = "Installation"
subtitle = ""

[sidebar]
  sticky = true
+++

<p>

### Download Knoxite

Make sure you have a working Go environment. Follow the [Go install instructions](http://golang.org/doc/install.html).

To install knoxite, simply run:

    go get github.com/knoxite/knoxite/cmd/...

To compile it from source:

    cd $GOPATH/src/github.com/knoxite/knoxite
    go get -u -v
    go build cmd/knoxite/ && go test -v

Run `knoxite --help` to see a full list of options.

</p>
