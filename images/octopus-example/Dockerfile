FROM ubuntu:18.04
ARG AZDFTools_Version=0.80
ARG Azure_Cli_Version=2.14.0\*
ARG Azure_Powershell_Version=6.4.0
#ARG Octopus_Cli_Version=7.4.1
#ARG Octopus_Client_Version=8.8.3
ARG Powershell_Version=7.0.6\*
  

# get `wget` & software-properties-common
# https://docs.microsoft.com/en-us/powershell/scripting/install/installing-powershell-core-on-linux?view=powershell-7#ubuntu-1804
RUN apt-get update && \
    apt-get install -y wget unzip apt-utils curl software-properties-common

# get powershell for 18.04 to support PowerShell scripts in execution container
RUN wget -q https://packages.microsoft.com/config/ubuntu/18.04/packages-microsoft-prod.deb && \
    dpkg -i packages-microsoft-prod.deb && \
    apt-get update && \
    add-apt-repository universe && \
    apt-get install -y powershell

# Get python & groff to support Python scripts in execution container
RUN apt-get install -y python3-pip groff

# Get Octo CLI
# https://octopus.com/downloads/octopuscli#linux
# RUN apt-get update && \
#     apt-get install -y --no-install-recommends gnupg curl ca-certificates apt-transport-https && \
#     curl -sSfL https://apt.octopus.com/public.key | apt-key add - && \
#     sh -c "echo deb https://apt.octopus.com/ stable main > /etc/apt/sources.list.d/octopus.com.list" && \
#     apt-get update && \
#     apt-get install -y octopuscli=${Octopus_Cli_Version}

# Install Octopus Client
# https://octopus.com/docs/octopus-rest-api/octopus.client
# RUN pwsh -c 'Install-Package -Force Octopus.Client -MaximumVersion "'${Octopus_Client_Version}'" -source https://www.nuget.org/api/v2 -SkipDependencies' && \
#     octopusClientPackagePath=$(pwsh -c '(Get-Item ((Get-Package Octopus.Client).source)).Directory.FullName') && \
#     cp -r $octopusClientPackagePath/lib/netstandard2.0/* .

# Get AZ Powershell core modules
# https://docs.microsoft.com/en-us/powershell/azure/install-az-ps?view=azps-3.6.1
RUN pwsh -c 'Install-Module -Force -Name Az -AllowClobber -Scope AllUsers -MaximumVersion "'${Azure_Powershell_Version}'"'

# Get Helm3
# RUN wget --quiet -O - https://raw.githubusercontent.com/kubernetes/helm/master/scripts/get | bash -s -- -v ${Helm_Version}

# Get Azure CLI
# https://docs.microsoft.com/en-us/cli/azure/install-azure-cli-apt?view=azure-cli-latest
RUN wget --quiet -O - https://packages.microsoft.com/keys/microsoft.asc | gpg --dearmor | tee /etc/apt/trusted.gpg.d/microsoft.asc.gpg > /dev/null && \
    echo "deb [arch=amd64] https://packages.microsoft.com/repos/azure-cli/ bionic main" | tee /etc/apt/sources.list.d/azure-cli.list && \
    apt-get update && \
    apt-get install -y azure-cli=${Azure_Cli_Version}

# Installing AZDFTools
RUN pwsh -Command "Install-Module -Force -Name azure.datafactory.tools -Scope AllUsers -MaximumVersion '$AZDFTools_Version'"
# RUN pwsh -Command "Import-Module Az"
# RUN pwsh -Command "Import-Module azure.datafactory.tools"


# Get NodeJS
# https://websiteforstudents.com/how-to-install-node-js-10-11-12-on-ubuntu-16-04-18-04-via-apt-and-snap/\
# RUN wget --quiet -O - https://deb.nodesource.com/setup_14.x | bash && \
#     apt-get install -y nodejs

# Get the Istio CLI
# https://istio.io/docs/ops/diagnostic-tools/istioctl/
# RUN curl -sL https://istio.io/downloadIstioctl | sh - && \
#     mv /root/.istioctl/bin/istioctl /usr/local/bin/istioctl && \
#     rm -rf /root/.istioctl

# Get the Linkerd CLI
# https://linkerd.io/2/getting-started/
# RUN curl -sL https://run.linkerd.io/install | sh && \
#     cp /root/.linkerd2/bin/linkerd /usr/local/bin && \
#     rm -rf /root/.linkerd2

# Get tools for working with Docker images without the Docker daemon
# https://github.com/openSUSE/umoci
# RUN curl --silent --location https://github.com/opencontainers/umoci/releases/download/v${Umoci_Version}/umoci.amd64 -o /usr/local/bin/umoci && \
#     chmod +x /usr/local/bin/umoci

# Get common utilities for scripting
# https://mikefarah.gitbook.io/yq/
# https://augeas.net/
# RUN add-apt-repository -y ppa:rmescandon/yq && \
#     apt-get update && apt-get install -y jq yq openssh-client rsync git augeas-tools

# Skopeo
# https://github.com/containers/skopeo/blob/master/install.md
# RUN sh -c "echo 'deb http://download.opensuse.org/repositories/devel:/kubic:/libcontainers:/stable/xUbuntu_18.04/ /' > /etc/apt/sources.list.d/devel:kubic:libcontainers:stable.list" && \
#     wget -nv https://download.opensuse.org/repositories/devel:kubic:libcontainers:stable/xUbuntu_18.04/Release.key -O- | apt-key add - && \
#     apt-get update && apt-get install -y skopeo
