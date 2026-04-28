# Gitops approach to host inventory promotion.

The rough idea is to seperate stages for host inventory into:

- Planned
- Validating
- Available
- Assigned

For Phases outside of Assigned, the resources I am thinking of using are Siteconfig centric

- `BareMetalHost`
- `HostFirmwareSettings`
- `FirmwareSchema`
- `HostFirmwareComponents`

The idea is that the infra teams would have inventory that is `planned` or potential to become a node or cluster in the future

The `validating` phase is where the above resources would be applied, think if setting defaults on hardware and confirming it meets whatever integrated hardware needs etc.

`Available` would be where the node meets whatever needs and is now ready to be adopted or pulled into whatever type, labeled for master or work or potentially both.

Finally, `Assigned` is where we transition the `Available` resource to a cluster-isntall type rather then just the individual nodes.  I may also do a lifecycle for cluster-install types as well but..

---

clusters/ is wher actual clusters live, they have consumed `Available` resources and converte them to `Assigned`

Resources

- `ClusterInstance`

(rendered)
- InfraEnv
- AgentClusterInstall


---

Functionality / Lifecycle.

The aproach is an app-of-apps that builds templates based upon resource naming conventions and file conventions in the files.  This allows you to just drag a resource from one stage to another triggering a delete in one folder and an add in another.  Thist allows to tie in gitocmmits etc.

