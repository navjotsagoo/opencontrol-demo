# Open Control - Accelerating ATO for mission capabilities

**Pre-Reqs:**
- [Compliance Masonry CLI](https://github.com/opencontrol/compliance-masonry/blob/master/docs/install.md)
- [GitBook CLI](https://github.com/GitbookIO/gitbook-cli)

Download this repository
```bash
git clone https://github.com/nsagoo-pivotal/opencontrol-demo.git
```

See the Minimum Number of Security Controls required for FedRAMP-low certification
```bash
compliance-masonry diff FedRAMP-low | grep "missing controls"
```
> > Number of missing controls: 125

Download Security Controls
```bash
compliance-masonry --verbose get
```

See the number of security controls satisfied
```bash
compliance-masonry diff FedRAMP-low
```
> > Number of missing controls: 0

Generate System Security Plan (SSP) Documentation
```bash
compliance-masonry docs gitbook FedRAMP-low
cd exports
gitbook serve
> Open browser at http://localhost:4000
```
The gitbook command by default will create a folder called exports that contains the files needed to create a gitbook. Use the gitbook to serve the content locally.

To deploy the SSP Documentation to Cloud Foundry
```bash
cd exports/_book
cf push ssp -b staticfile_buildpack
```

## Options

Starting with a basline where 0 security controls are satisfied for FedRAMP-low accreditation.
```bash
compliance-masonry diff FedRAMP-low | grep "missing controls"
> Number of missing controls: 125
```

Inherit Infrastructure Security Controls
```bash
compliance-masonry get --config manifests/infrastructure-security-controls.yml
compliance-masonry diff FedRAMP-low | grep "missing controls"
> Number of missing controls: 117
```
Infrastructure satisfied `8` security controls.

Inherit Cloud Foundry and Infrastructure Security Controls
```bash
compliance-masonry get --config manifests/cloud-foundry-security-controls.yml
compliance-masonry diff FedRAMP-low | grep "missing controls"
> Number of missing controls: 9
```
Cloud Foundry alone satisfied `108` security controls.

Together, Infrastructure & Cloud Foundry satisfy 116 security controls.

Inherit Application, Cloud Foundry, and Infrastructure Security Controls
```bash
compliance-masonry get --config manifests/application-security-controls.yml
compliance-masonry diff FedRAMP-low | grep "missing controls"
> Number of missing controls: 0
```
Given that Cloud Foundry and Infrastructure satisfied most of the security controls, the application had to only satisfy 9 security controls. It inherited the remaining security controls directly from the platform and infrastructure. Once those 9 security controls are satisfied, then application can be considered in full compliance and use opencontrol to generate SSP for its certification and accreditation.
