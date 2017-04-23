# Open Control - Accelerating the ability to achieve ATO for mission capabilities

Pre-Reqs:
[Compliance Masonry CLI](https://github.com/opencontrol/compliance-masonry/blob/master/docs/install.md)
[GitBook CLI](https://github.com/GitbookIO/gitbook-cli)

```bash
git clone https://github.com/nsagoo-pivotal/opencontrol-demo.git
```

See the Minimum Number of Security Controls required for FedRAMP-low certification
```bash
compliance-masonry diff FedRAMP-low | grep "missing controls"
```
> 125 Missing Controls

Download Security Controls
```bash
compliance-masonry --verbose get
```

See the number of security controls satisfied
```bash
compliance-masonry diff FedRAMP-low
```
> 0 missing controls!

Generate System Security Plan (SSP) Documentation
```bash
compliance-masonry docs gitbook FedRAMP-low
cd exports
gitbook serve
> Open http://localhost:4000
```
The gitbook command by default will create a folder called exports that contains the files needed to create a gitbook. Use the gitbook to serve the content locally. 

## Options

Inherit Infrastructure Security Controls
```bash
compliance-masonry --verbose get --config manifests/infrastructure-security-controls.yml
```

Inherit Cloud Foundry and Infrastructure Security Controls
```bash
compliance-masonry --verbose get --config manifests/cloud-foundry-security-controls.yml
```

Inherit Application, Cloud Foundry, and Infrastructure Security Controls
```bash
compliance-masonry --verbose get --config manifests/application-security-controls.yml
```
