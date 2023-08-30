**Creating an Image with DD**
Basic Syntax
`dd if=<input device> of=<output device/image name> [options]`
- of equal output devices
- Other options ...
	- bs=16M
		- bs equal block size, not to be confused with sector size
	- conv=noerror,sync
		- conv == convert the file, in this case we ignore errors
		- sync == pads the blocks with zeros so the images offsets stay in sync with the original
	- status=progress

If we wanted to output afile to the /tmp folder, we would use the following command
`dd if=/dev/sda of=/tmp/data_aqc.dd bs=16M conv=noerror,sync status=progress`

**Compressing the image into an E01**
We use FTK imager to convert to the E01 format, which is essentially just a compressed DD file.

`ftkimager /tmp/data_aqc.dd /tmp/data_aqc --e01`

Alternatively, we could just zip the DD image
`gzip -k data_aqc_linux.dd`

Combining the previous commands with a pipe will make it seamless to create a zipped DD file
`dd if=/dev/sda bs=16 conv=noerror,sync status=progress | gzip -c > /tmp/data_aqc.dd.gz`

