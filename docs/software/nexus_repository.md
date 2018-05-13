### Introduction 

This is supposed to be a free alternative to Artifactory that has Docker support and PYPI support. There are also community plugins for CRAN too. 

  - https://gist.github.com/diegopacheco/0d6dcb6771166a87d5eb
  - https://asadbukhariblog.wordpress.com/2015/08/31/sonatype-nexus-oss-installation-on-ubuntu-14-04-lts/
  - https://www.build-business-websites.co.uk/install-nexus-on-ubuntu-16-04/
  - https://help.sonatype.com/repomanager3/configuration
  - https://help.sonatype.com/repomanager3/private-registry-for-docker
  - https://help.sonatype.com/repomanager3/pypi-repositories

This requires SSL certification to setup properly. Probably just going to use Docker's built in private registry on the host VM, so long as images are pulled from that same machine it should be fine. Probably requires that we set jenkins up on that server as well?