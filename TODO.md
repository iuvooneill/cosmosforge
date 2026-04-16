# TODOs

A bucket policy can be used to restrict downloads to known IPs. Technically only "ks/" needs to be restricted with the sensitive data (encrypted though - it's primarily the ansible ssh public key and the root PW crypt if used). The ipxe/default.ipxe doesn't contain sensitive info, but contains the location of the given kickstart and we could have system-specific files that might give internal organization info. boot/ only contains OS boot files.

More complicated authentication rules would require a web server that we can control, or CloudFront.

# iPXE

We can write the iPXE config file to get the default.ipxe file...can we use ansible to build the ISO?

Can we create a more complex iPXE config that can boot system-specific profiles?

This might be a good use of a workflow.
