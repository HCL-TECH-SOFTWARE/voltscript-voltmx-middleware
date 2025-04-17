# What's new

The section provides information on the latest features, improvements, and resolved issues related to VoltScript Volt MX Middleware.

<!-- prettier-ignore -->
!!! note "Important"
    - Items marked in <span style="color:red">**red**</span> are API changes that may impact your applications and should be reviewed before upgrading.

???+ info "v1.0.5 - What's new or changed"

    ## v1.0.4
    **Improvements**
    - <span style="color:red">Integration with VoltScript Logging</span>
    - <span style="color:red">Repointing atlas.json to demo marketplace. atlas-settings marketplace url will need updating to "https://accounts.auth.demo-hclvoltmx.net/login".</span>

???+ info "v1.0.4 - What's new or changed"

    ## v1.0.4
    **Improvements**

    - <span style="color:red">Repointing atlas.json to use VSE title and filename as library and module.</span>
    - Documentation improvements.

???+ info "v1.0.1 - What's new or changed"
    ## v1.0.1
    **Improvements**

    - Added jsonSort function and associated classes.
    - Added VSID database to repo. **NOTE:** jsonComparator class is not set to derived in NSF because of [VSID issue](https://github.com/HCL-TECH-SOFTWARE/voltscript-interface-designer/issues/1). If code is regenerated from NSF, class signature and constructor signature require manual fixup.
    - <span style="color:red">Repointing atlas.json from demo marketplace. atlas-settings marketplace url will need updating to "https://accounts.auth.hclvoltmx.net/login".</span>
    - <span style="color:red">Amended addDeviceHeader() methods to take a string.</span>

??? info "v1.0.0 - What's new or changed"
    ## v1.0.0

    - First release version of VoltScript Volt MX Middleware.