# Docker image for MATLAB license manager (lmgrd)

This repo hosts the matlab license server deployment.

The deployment requires a license.dat file:
```text
# BEGIN--------------BEGIN--------------BEGIN
# MathWorks license passcode file.
# LicenseNo: ***   HostID: {{ container MAC address}}
#
# R***
#
SERVER {{ hostname }} {{ container MAC address}} {{ lmgrd port }}
DAEMON MLM /lmgrd/etc/glnxa64/MLM port={{ mlm port }}
INCREMENT <<License information>>
# END-----------------END-----------------END
```

The `{{}}` placeholders have to fit with the docker-compose configuration

For further explanation, refer to the [manual](https://www.mathworks.com/matlabcentral/answers/uploaded_files/5871/LicenseAdministration.pdf). `LICENSEDIR` is where you store your license manager. You could easily update the license file without rebuild the Docker image. You might need to restart the Docker container if needed.

For client who need to use this lmgrd, they could use a simple license file:

```text
SERVER 192.168.99.10 INTERNET=192.168.99.10 27000
USE_SERVER
```
