
Basic Docker image of the adapter using a nightly build

* Generally installed to /opt/interlok
* Various distribution platforms are defined in the corresponding sub directories.

## Notes

This image does not expose any ports or volumes; so you will need to expose those yourself when building your own docker image.

Our suggestions would be to

* Expose ports 8080 + 5555
* Volumes :
    * /opt/interlok/config -> for layering in your own configuration
    * /opt/interlok/logs  -> for logging; if you're using log4j logging to diskk
    * /opt/interlok/ui-resources -> for preserving templates and saved projects.


