# Release notes

This topic contains release notes for Tanzu Application Platform v1.4.

## <a id='1-4-0'></a> v1.4.0

**Release Date**: January 10, 2023

### <a id="1-4-0-tap-new-features"></a> Tanzu Application Platform new features

- [Shared Ingress Issuer](security-and-compliance/ingress-certificates.hbs.md) for secure ingress
  communication by default. [CNRs](cloud-native-runtimes/about.hbs.md), [AppSSO](app-sso/about.hbs.md),
  and [Tanzu Application Platform GUI](tap-gui/about.hbs.md) use this issuer to secure
  ingress. In future releases, all Tanzu Application Platform components will be incrementally updated
  to support the shared ingress issuer.
- [Namespace Provisioner](namespace-provisioner/about.hbs.md) provides a secure, automated
  way for Platform Operators to provision namespaces with the resources and proper namespace-level
  privileges required for their workloads to function as intended.
- [Tanzu Application Platform Telemetry Reports](telemetry/overview.hbs.md#tanzu-application-platform-usage-reports)
  offers the option to enroll in a usage reporting program that provides a usage summary of your
  Tanzu Application Platform.
- [Tanzu Developer Tools for Visual Studio](vs-extension/about.hbs.md) is an IDE extension for
  Visual Studio to help you develop, providing the rapid iteration experience for .NET Core apps in
  Tanzu Application Platform.

</br>

---

</br>

### <a id='1-4-0-new-component-features'></a> New features by component and area

#### <a id="1-4-0-appsso-nf"></a> Application Single Sign-On (AppSSO)

- Added ability to configure custom Redis storage for an `AuthServer` by
  using a ProvisionedService-style API. For more information, see
  [Storage](app-sso/service-operators/storage.hbs.md).
- Added package field `default_authserver_clusterissuer` that inherits
  the `shared.ingress_issuer` value from Tanzu Application Platform if not set.
  For more information, see [IssuerURI and TLS](app-sso/service-operators/issuer-uri-and-tls.hbs.md).
- Added `AuthServer.spec.tls.deactivated` to deprecate `AuthServer.spec.tls.disabled`.
- `AuthServer.spec.tokenSignatures` is now a required field.
- In addition to globally trusted CA certificates, granular trust can be extended with `AuthServer.spec.caCerts`.
- LDAP is now a supported identity provider protocol. For more information, see [LDAP](app-sso/service-operators/identity-providers.hbs.md#ldap).
  - LDAP bind is validated on `AuthServer` creation when an LDAP identity provider is defined.
  - Introduced `identityProviders.ldap.url` in `AuthServer.spec`.
  - Introduced `identityProviders.ldap.group.search`.
  - `identityProviders.ldap.group` is now optional in `AuthServer.spec`.
</br></br>

#### <a id="1-4-0-app-live-view"></a> Application Live View

- Users can now activate or deactivate the automatic configuration of Spring Boot actuators on Tanzu Application Platform and on workloads.
  For more information, see [Configure and access Spring Boot actuators in Tanzu Application Platform](spring-boot-conventions/configuring-spring-boot-actuators.hbs.md).
- Added App Live View Memory View panel in Visual Studio Code as part of Spring Boot Dashboard extension.
- Added support for Spring Boot 3. Spring Boot 3 Native Image is not supported.
- Added new App Live View pages `HTTP Requests` and `Request Mappings` for Steeltoe workloads.
- Added `appliveview_connnector.backend.sslDeactivated` to deprecate `appliveview_connnector.backend.sslDisabled`.
</br></br>

#### <a id="1-4-0-app-accelerator"></a> Application Accelerator

- Optional Git repository creation during project generation is supported in the Application Accelerator extension for VS Code.
  - The parameter [`.app_config.gitProviders.active` in `tap-values.yaml`](tap-gui/plugins/application-accelerator-git-repo.hbs.md#deactiv-git-repo-creation) was added to deactivate optional Git repository creation in the VS Code extension during project creation.
- Added [custom `types`](application-accelerator/creating-accelerators/custom-types.hbs.md) which allows for 1-N number of repeating sets of options in an accelerator's form during project creation.
- Added the [Loop transform](application-accelerator/creating-accelerators/transforms/loop.hbs.md) to allow for transforms to be applied on list options.
- Added [`generate-from-local`](cli-plugins/accelerator/command-reference/tanzu_accelerator_generate_from_local.hbs.md) command to the Application Accelerator plug-in for the Tanzu CLI to generate accelerators using local assets without needing to commit code.
- Additional Application Accelerator plug-ins for Tanzu CLI improvements:
  - `fragment create` now supports `--local-path` and `--source-image`
  - `fragment update` now supports `--source-image`
- Application Accelerator Samples:
  - **Accelerators** - the following accelerators were added:
    - [Angular Frontend Accelerator](https://github.com/vmware-tanzu/application-accelerator-samples/tree/main/angular-frontend) - quickly bootstrap an Angular-based Single Page App
    - [React Frontend Accelerator](https://github.com/vmware-tanzu/application-accelerator-samples/tree/main/react-frontend) - quickly bootstrap a React-based Single Page App
  - **Fragments** - the following fragments were added:
    - [Spring Boot H2 Fragment](https://github.com/vmware-tanzu/application-accelerator-samples/tree/main/fragments/spring-boot-h2)
    - [Spring Boot MySQL Fragment](https://github.com/vmware-tanzu/application-accelerator-samples/tree/main/fragments/spring-boot-mysql)
    - [Spring Boot PostgreSQL Fragment](https://github.com/vmware-tanzu/application-accelerator-samples/tree/main/fragments/spring-boot-postgresql)
</br></br>

#### <a id="1-4-0-cert-manager"></a> cert-manager

- `cert-manager.tap.tanzu.vmware.com` can optionally install self-signed `ClusterIssuer`s.
</br></br>

#### <a id="1-4-0-eventing"></a> Eventing

- Upgraded Knative Eventing version from 1.6 to 1.8.
- Added a Kubernetes tracing attribute to ApiServerSource.
- The ApiServerSource is a Knative Eventing Kubernetes custom resource that listens for events emitted by the Kubernetes API server (eg. pod creation, deployment updates, etc...) and forwards them as CloudEvents to a sink.
</br></br>

#### <a id="1-4-0-tap-gui-plugin-nf"></a> External Secrets Operator (alpha)

- The External Secrets Operator is a Kubernetes operator that integrates with external secret management systems.
  With this release, Tanzu Application Platform repackages this open source Kubernetes operator into a Carvel bundle that ships with Tanzu Application Platform. **External Secrets Operator is currently in alpha and is intended for evaluation and test purposes only. Do not use in a production environment.**

#### <a id="1-4-0-stk-new-features"></a> Services Toolkit

- Added new `ClassClaim` API that allows claims for service instances to be created by referring to
  a `ClusterInstanceClass`. For more information, see
  [When to use ClassClaim vs ResourceClaim](https://docs-staging.vmware.com/en/draft/Services-Toolkit-for-VMware-Tanzu-Application-Platform/0.9/svc-tlk/GUID-resource_claims-which_claim.html)
  and [Introducing different service implementations in different environments](https://docs-staging.vmware.com/en/draft/Services-Toolkit-for-VMware-Tanzu-Application-Platform/0.9/svc-tlk/GUID-usecases-introducing_different_service_implementations_in_different_environments.html).
- Added corresponding `tanzu services class-claims` CLI plug-in command.
- Added support for OpenShift v4.11.
- Added support for Kubernetes v1.25.
- All containers are now configured with read-only root file systems.

#### <a id="1-4-0-tap-gui-plugin-nf"></a> Tanzu Application Platform GUI Plug-ins

##### <a id='scc-plug-in-new-features'></a>Supply Chain Choreographer Plug-in

- Events are now emitted when resources are applied and when their output or health status changes.
  See [Events reference](scc/events.hbs.md).
- Source Tester stage now includes a link to the Jenkins job when Jenkins is configured for use
  in the supply chain.
- `spec.source.git.url` is added to the Overview section of the Source Provider stage in the
  supply chain.
- Added support to include current and historical Kaniko build logs in the Stage Details section of
  the supply chain when Kaniko is used as the build service in the Image Provider stage.
- Scanning stages now include a `Show Unique CVEs` filter so that the scan results show one CVE
  per ID as opposed to each CVE per package.
  This allows better alignment between the data in the Supply Chain Choreographer plug-in and the
  Security Analysis plug-in.
</br></br>

##### <a id='1-4-0-sagui-new-feats'></a>Security Analysis Plug-in

- **Understand the total number of affected packages and vulnerabilities on the
  Security Analysis Dashboard:** The Vulnerabilities by Severity widget and the
  Workload Build Vulnerabilities table have updated logic to count all CVEs and
  packages, providing a better idea of the discrete, affected packages.
  Previously, the logic counted unique CVEs, even if a particular CVE affected
  multiple packages.
- **Quickly identify all affected workloads for a specific CVE, package or
  dependency:** The CVE and Package details pages include a new table which
  shows all affected workloads for a specific CVE or package. You access the CVE
  and Package details page on the source or image scan stage in the Supply Chain
  Choreographer Plug-in.
</br></br>

#### <a id="1-4-0-scst-scan-new-features"></a> Supply Chain Security Tools - Scan

- Users no longer need to create a package overlay to enable Grype in offline and air-gapped
  environments. See [Using Grype in offline and air-gapped environments](scst-scan/offline-airgap.hbs.md).
- Increased compatibility with customers' existing environments by supporting custom certificate authorities (CAs) via the tap-values.yml for both Grype and Snyk scanners.
- Alpha release of Prisma Scanner integration. The installation guide is available [here](scst-scan/install-prisma-integration.hbs.md).
</br></br>

#### <a id="1-4-0-scst-policy-new-features"></a> Supply Chain Security Tools - Policy

- Added ability to [configure action when no policy matches the admitting image digest](./scst-policy/install-scst-policy.hbs.md#install-scst-policy).
- Added ability to [allow empty authorities for ClusterImagePolicies](./scst-policy/install-scst-policy.hbs.md#install-scst-policy).
- Added ability to [specify which resources a ClusterImagePolicy should enforce](./scst-policy/configuring.hbs.md#cip-match).
</br></br>

#### <a id="1-4-0-vscode-new-features"></a> Tanzu Developer Tools for Visual Studio Code

- The developer sandbox enables developers to Live Update their code, and
  simultaneously debug the updated code, without having to deactivate Live Update when debugging.
</br></br>

#### <a id="1-4-0-vs-new-features"></a> Tanzu Developer Tools for Visual Studio

- **See code updates running on-cluster in seconds:**
  By using Live Update facilitated by Tilt, deploy your workload once, save changes to the code
  and then, seconds later, see those changes reflected in the workload running on the cluster.
  All Live Update output is filtered to its own output pane window within Visual Studio.

- **Debug workloads directly on the cluster:**
  Debug your application in a production-like environment by debugging on your Kubernetes cluster that
  has Tanzu Application Platform. An environment’s similarity to production relies on keeping
  dependencies updated, among other variables.

#### <a id="1-4-0-api-validation-and-scoring"></a> API Validation and Scoring Toolkit

- API Validation and Scoring focuses on scanning and validating an OpenAPI specification. The API
  specification is generated from the API Auto Registration of Tanzu Application Platform. See [API
  Validation and Scoring](api-validation-scoring/about.hbs.md) for more information.
</br></br>

#### <a id="1-4-0-intellij-new-feat"></a> Tanzu Developer Tools for IntelliJ

- The developer sandbox enables developers to Live Update their code, and
  simultaneously debug the updated code, without having to deactivate Live Update when debugging.
- An Activity pane was added in the Tanzu Panel which allows developers to visualize the supply
  chain, delivery, and running application pods.
  It displays detailed error messages on each resource and enables developers to describe and view
  logs on these resources from within their IDE.
- Tanzu workload `apply` and `delete` actions were added to ​IntelliJ.
- Code snippets to create `workload.yaml` and `catalog-info.yaml` files were added to IntelliJ.
</br></br>

#### <a id="1-4-0-apps-cli-plugin-new-feat"></a> Apps plugin for Tanzu CLI

- Added `--update-strategy` flag to allow users to change `tanzu apps workload apply` behavior when
  contents from file is applied.
- Added ability for users to pass URL for `--file` flag.
- Added show fully qualified resource name in the resources column of Supply chain and Delivery
  sections of the `tanzu apps workload get` command.
- Added new shorthand flag aliases: `-a` for `--app`, `-e` for `--env`, `-i` for `--image`,
  `-l` for `label`, `-p` for `--param`, and `-t` for `--type`.
- Added emojis to `tanzu apps workload create/apply/delete` commands.
- Added do not print emojis when `--no-color` flag  is set.
- Added namespace to `tanzu apps workload get` command's overview section.
- Added progress bar to provide feedback to users when uploading source code to registry.
- Added remove color from tail command output when `--no-color` flag is passed.

</br>

---

</br>

### <a id='1-4-0-breaking-changes'></a> Breaking changes

This release has the following breaking changes, listed by area and component.

#### <a id="1-4-0-appsso-bc"></a> Application Single Sign-On (AppSSO)

- Removed `AuthServer.spec.identityProvider.ldap.group.search{Filter,Base,Depth,SubTree}` and
  introduced `ldap.group.search: {}`.
  - If `ldap.group` is defined and `ldap.group.search` is not defined, the LDAP is considered
      an ActiveDirectory style LDAP and groups are loaded from the user's `memberOf` attribute.
  - If `ldap.group` and `ldap.group.search` are both defined, the LDAP is considered a Classic
      LDAP and group search is done by searching in the `ldap.group.search.base`.
  - There used to be a mixed mode, when both searches were attempted every time.
- Removed `AuthServer.spec.identityProviders.ldap.server` field.
- Removed `AuthServer.status.deployments.authServer.lastParentGenerationWithRestart` field.
- Removed deprecated field `AuthServer.spec.issuerURI`. For more information, see [IssuerURI and TLS](./app-sso/service-operators/issuer-uri-and-tls.hbs.md).
</br></br>

#### <a id="1-4-0-supply-chain-templates"></a> Out of the Box Supply Chain Templates

In a multicluster setup, when a Deliverable is created on a Build profile cluster,
the ConfigMap it is placed in is renamed from `<workload-name>` to `<workload-name>-deliverable`. Any automation
depending on obtaining the Deliverable content by the former name must be updated to use the new name.
For more information, see [Multicluster Tanzu Application Platform overview](multicluster/about.hbs.md).

#### <a id="1-4-0-intellij-bc"></a> Tanzu Developer Tools for IntelliJ

- IntelliJ IDEA v2022.2 to v2022.3 is required to install the extension.
</br></br>

#### <a id="1-4-0-vscode-bc"></a> Tanzu Developer Tools for Visual Studio Code

- `Tanzu Debug` no longer port forwards the application port (8080).
</br></br>

#### <a id="1-4-0-tap-gui-bc"></a> Tanzu Application Platform GUI

- **Ingress URL:** As mentioned in the [new features section](#1-4-0-tap-new-features),
  Tanzu Application Platform GUI participates in the shared ingress issuer feature.
  You might need to change your scheme from http to https. For more information, see
  [Troubleshooting](tap-gui/troubleshooting.hbs.md#catalog-not-loading).

- **Communication with Supply Chain Security Tools - Store:**
  In previous versions of Tanzu Application Platform, you configured Tanzu Application Platform GUI
  to use the read-only access token to communicate with Supply Chain Security Tools - Store.

  In v1.4, you must use the read-write access token to use new features in the Security Analysis GUI
  plug-in. If upgrading from v1.3, update your Tanzu Application Platform GUI configuration accordingly.
  See the updated instructions in [Enable CVE scan results](tap-gui/plugins/scc-tap-gui.hbs.md#scan).

#### <a id="1-4-0-scst-scan-bc"></a> Supply Chain Security Tools - Scan

- **Deprecated and removed ScanTemplates:**

  Deprecated Grype ScanTemplates shipped with Tanzu Application Platform v1.1 and earlier are
  removed and no longer supported. Use Grype ScanTemplates v1.2 and later.

- **Deprecation notice for `docker` field and related sub-fields:**

  The `docker` field and related sub-fields used in Supply Chain Security Tools - Scan are
  deprecated and marked for removal in Tanzu Application Platform v1.7.0.
  The deprecation impacts Scan Controller, Grype Scanner, and Snyk Scanner.
  Carbon Black Scanner is not impacted.
  For information about the migration path, see
  [Troubleshooting](scst-scan/observing.hbs.md#unable-to-pull-scanner-controller-images).
</br></br>

#### <a id="1-4-0-ipw-bc"></a> Supply Chain Security Tools - Image Policy Webhook

The Image Policy Webhook component is removed in Tanzu Application Platform v1.4. This component is deprecated
in favor of the [Policy Controller](./scst-policy/overview.hbs.md).
</br></br>

#### <a id="1-4-0-policy-controller-bc"></a> Supply Chain Security Tools - Policy Controller

Policy Controller no longer initializes TUF by default. TUF is required to
support the keyless authorities in `ClusterImagePolicy`. To continue to use
keyless authorities, provide the value `policy.tuf_enabled:
true` by using the `tap-values.yaml` while upgrading. By default,
the public Sigstore The Update Framework (TUF) server is used. To
target an alternative Sigstore stack, specify `policy.tuf_mirror` and
`policy.tuf_root`.

</br>

---

</br>

### <a id='1-4-0-security-fixes'></a> Security fixes

This release has the following security fixes, listed by area and component.

#### <a id='1-4-0-scst-grype-fixes'></a> Supply Chain Security Tools - Grype

- `python` is updated to `3.7.5-22.ph3`.
</br></br>

#### <a id="1-4-0-api-auto-registration-fixes"></a> API Auto Registration

- Base image updated to use the latest Paketo Jammy Base image.

</br>

#### <a id="1-4-0-vulnerabilities-remediated"></a> Remediated vulnerabilities

Here is a list of vulnerabilities that are remediated with this release:</br>

- GHSA-7hfm-57qf-j43q, GHSA-crv7-7245-f45f, GHSA-mc84-pj99-q6hh, GHSA-xqfj-vm6h-2x34, CVE-2022-42003, CVE-2022-42004, GHSA-jjjh-jjxp-wpff,
GHSA-rgv9-q543-rqg4, GHSA-3mc7-4q67-w48m, GHSA-36p3-wjmg-h94x, CVE-2022-23960, CVE-2022-43945, GHSA-crp2-qrr5-8pq7, GHSA-7qw8-847f-pggm,
GHSA-c3xm-pvg7-gh7r, GHSA-f524-rf33-2jjr, CVE-2022-2509, CVE-2022-3171, CVE-2022-3509, CVE-2022-3510, GHSA-4gg5-vx3j-xwc7, GHSA-g5ww-5jh7-63cx,
GHSA-66x3-6cw3-v5gj, CVE-2022-3515, CVE-2022-2602, CVE-2022-41222, CVE-2022-32212, CVE-2022-35255, CVE-2021-27478, CVE-2021-27482,
CVE-2021-27498, CVE-2021-27500, CVE-2019-12900, CVE-2021-28861, CVE-2021-3737, CVE-2022-0391, GHSA-4w2j-2rg4-5mjw, CVE-2022-2586,
CVE-2022-2588, CVE-2022-34918, GHSA-4wf5-vphf-c2xc, CVE-2022-42916, CVE-2022-43551, CVE-2022-43552, CVE-2021-3999, GHSA-m974-647v-whv7

</br>

---

</br>

### <a id='1-4-0-resolved-issues'></a> Resolved issues

The following issues, listed by area and component, are resolved in this release.

#### <a id="1-4-0-api-auto-registration-ri"></a> API Auto Registration

- API Auto Registration periodically checks the original API specification from the defined
  location to find changes and registers any changes into the `API Descriptor`. This triggers
  reconciliation into the Tanzu Application Platform GUI catalog. This synchronization period or
  frequency is configurable through the new value `sync_period`. The default value is 5 minutes.
</br></br>

#### <a id="1-4-0-appsso-ri"></a> Application Single Sign-On (AppSSO)

- Fixed infinite redirect loops for an `AuthServer` configured with a single OIDC or SAML identity provider.
- Authorization Code request rejected audit event from anonymous users logging proper IP address.
- `AuthServer` no longer attempts to configure Redis event listeners.
- OpenShift: custom `SecurityContextConstraint` resource is created for Kubernetes platforms
  versions 1.23.x and lower.
- LDAP error log now contains proper error message.
</br></br>


#### <a id="1-4-0-supply-chain-templates-resolved"></a> Out of the Box Supply Chain Templates

Fixed deliverable content written into ConfigMaps in multicluster setup:

- ConfigMap is renamed to avoid conflict with `config-template`.
- Labels to attribute the Deliverable content with the supply chain and template are now added to be consistent with the ordinary Delivery on a non-Build profile cluster.

For more information, see [Multicluster Tanzu Application Platform overview](multicluster/about.hbs.md).

#### <a id="1-4-0-apps-cli-plugin-ri"></a> Tanzu CLI Apps Plug-in

- Fixed `tanzu apps workload tail` command output, which was displaying extra init container log lines.
- Fixed `tanzu apps workload tail` command not including all logs.
</br></br>

#### <a id="1-4-0-tap-gui-plugin-ri"></a> Tanzu Application Platform GUI plug-ins

- **Immediate entity provider backend plug-in**

  - The entity provider, used mainly by API Auto Registration, now allows a body size of `5Mb` to
    accept larger API specifications.
  - Considering the restriction of Backstage for [Entity Provider mutations](https://backstage.io/docs/features/software-catalog/external-integrations#provider-mutations),
    whenever an existing entity is intended for a mutation through this plug-in, and its origin is
    a different entity provider, a `409 Conflict` error is returned.
</br></br>

#### <a id="supply-chain-plugin-ri"></a> Supply Chain Choreographer Plug-In

- The UI no longer shows the error `Unable to retrieve details from Image Provider Stage` when the
  Builder is not available or configured. It now correctly shows the same error as the CLI,
  `Builder default is not ready`.

</br>

---

</br>

### <a id='1-4-0-known-issues'></a> Known issues

This release has the following known issues, listed by area and component.

#### <a id="1-4-0-app-acc-vscode-ki"></a> Application Accelerator for Visual Studio Code

- When using custom types, if there is a check box in the list of attributes then re-ordering
  the inputs doesn't work.

#### <a id="1-4-0-cnr-ki"></a> Cloud Native Runtimes for VMware Tanzu

- Knative Serving: Certain app name, namespace, and domain combinations produce invalid HTTPProxy resources. See [Cloud Native Runtimes Troubleshooting](https://docs.vmware.com/en/Cloud-Native-Runtimes-for-VMware-Tanzu/2.1/tanzu-cloud-native-runtimes/GUID-troubleshooting.html#invalid-httpproxy).
- Knative Serving and Cert Manager: When auto-tls is enabled, the default in Tanzu Application Platform v1.4.0, Knative services fail with `certificateNotReady` if workload name, namespace, and domain are more than 64 bytes. See [Cloud Native Runtimes Troubleshooting](https://docs.vmware.com/en/Cloud-Native-Runtimes-for-VMware-Tanzu/2.1/tanzu-cloud-native-runtimes/GUID-troubleshooting.html#certificate-not-ready).

#### <a id="1-4-0-intellij-ki"></a> Tanzu Developer Tools for IntelliJ

- If a workload is deployed onto a namespace by using Live Update, you must set that namespace as
  the namespace of the current context of your kubeconfig file.
  Otherwise, if you run Tanzu Debug it causes the workload to re-deploy.
  For more information, see
  [Troubleshooting](intellij-extension/troubleshooting.hbs.md#debug-reapplies-apply).

- On macOS, Tanzu Panel might be empty when using a GKE cluster. For more information, see
  [Troubleshooting](intellij-extension/troubleshooting.hbs.md#panel-empty-gke).

- The **Describe** action in the pop-up menu in the Activity panel can fail when used on PodIntent
  resources. For more information, see
  [Troubleshooting](intellij-extension/troubleshooting.hbs.md#describe-action-fail).

- The Tanzu panel might show workloads without showing Kubernetes resources in the center panel of the
  activity pane. For more information, see
  [Troubleshooting](intellij-extension/troubleshooting.hbs.md#tnz-panel-k8s-rsrc-fail).

- The Details table and Messages pane in the activity panel can show stale data because these views
  only refresh when the selection in the Resource tree is changed.
  As a workaround, make the views refresh by clicking somewhere in the Resource tree to change the
  current selection.

#### <a id="1-4-0-vs-ki"></a> Tanzu Developer Tools for Visual Studio

- The `Tanzu: Delete Workload` command can fail with the extension erroneously reporting that the
  workload isn't running. For more information, see
  [Troubleshooting](vs-extension/troubleshooting.hbs.md#del-wrkld-not-running).

- The `Tanzu: Start Live Update` command can fail because the specified path was not found.
  For more information, see [Troubleshooting](vs-extension/troubleshooting.hbs.md#lv-update-path-not-found).

#### <a id="1-4-0-grype-scan-known-issues"></a>Grype scanner

**Scanning Java source code that uses Gradle package manager might not reveal vulnerabilities:**

For most languages, Source Code Scanning only scans files present in the source code repository.
Except for support added for Java projects using Maven, no network calls fetch
dependencies. For languages using dependency lock files, such as Golang and Node.js, Grype uses the
lock files to check dependencies for vulnerabilities.

For Java using Gradle, dependency lock files are not guaranteed, so Grype uses dependencies
present in the built binaries, such as `.jar` or `.war` files.

Because VMware discourages committing binaries to source code repositories, Grype fails to
find vulnerabilities during a source scan.
The vulnerabilities are still found during the image scan after the binaries are built and packaged
as images.
</br></br>

#### <a id="1-4-0-tap-gui-plugin-ki"></a> Tanzu Application Platform GUI plug-ins

##### <a id="supply-chain-plugin-ki"></a> Supply Chain Choreographer plug-in

- The `Generation` field and scan policy link in the **Overview** section does not update when you amend a scan policy. The correct version and details of the policy are shown in the CLI.
- Customizing the `Source Tester` stage in an OOTB supply chain does not show details in the
  **Stage Details** section.
- When a GitOps PR flow is configured, the **Approve a Request** link no longer appears in the supply chain graph.
</br>

##### <a id="sec-analysis-plugin-ki"></a> Security Analysis plug-in

- The **No Associated Policy** tab in Workload Build Vulnerabilities does not show workloads that lack
  associated scan policies.
- The CVEs bar graph in Workload Build Vulnerabilities sometimes cuts numbers off.

</br>

---

</br>

### <a id='1-4-0-deprecations'></a> Deprecations

The following features, listed by component, are deprecated.</br>
Deprecated features will remain on this list until they are retired from Tanzu Application Platform.</br></br>

#### <a id="1-4-0-app-sso-deprecations"></a> Application Single Sign-On (AppSSO)

- `AuthServer.spec.tls.disabled` is deprecated and marked for removal in the next release. For more
  information about how to migrate
  to `AuthServer.spec.tls.deactivated`, see [Migration guides](app-sso/upgrades/index.md#migration-guides).
</br></br>

#### <a id="1-4-0-app-live-view-deprecations"></a> Application Live View

- `appliveview_connnector.backend.sslDisabled` is deprecated and marked for removal in Tanzu Application Platform 1.7.0.
  For more information on the migration, see [Deprecate the sslDisabled key](app-live-view/install.hbs.md#deprecate-the-ssldisabled-key).
</br></br>

#### <a id="1-4-0-stk-deprecations"></a> Services Toolkit

- The `tanzu services claims` CLI plug-in command is now deprecated.
  It is hidden from help text output, but continues to work until officially removed after the
  deprecation period. The new `tanzu services resource-claims` command provides the same functionality.

#### <a id="1-4-0-ipw-dep"></a> Supply Chain Security Tools - Image Policy Webhook

The Image Policy Webhook component is removed in Tanzu Application Platform v1.4. This component is deprecated
in favor of the [Policy Controller](./scst-policy/overview.hbs.md).
</br></br>

#### <a id="1-4-0-scst-scan-deprecations"></a> Supply Chain Security Tools - Scan

- Removed deprecated ScanTemplates:
  - Deprecated Grype ScanTemplates shipped with versions prior to Tanzu Application Platform 1.2.0
    have been removed and are no longer supported. Please ensure you are using Grype ScanTemplates
    v1.2+ moving forward.
  - `docker` field and related sub-fields by Supply Chain Security Tools - Scan are deprecated and
    marked for removal in Tanzu Application Platform 1.7.0.
    - The deprecation will impact the following components: Scan Controller, Grype Scanner, and Snyk Scanner.
    - See [troubleshooting](scst-scan/observing.hbs.md#unable-to-pull-scanner-controller-images)
      documentation for the migration path.
</br></br>

#### <a id="1-3-scst-sign-deprecations"></a> Supply Chain Security Tools - Sign

- [Supply Chain Security Tools - Sign](scst-sign/overview.md) is deprecated. For migration
  information, see [Migration From Supply Chain Security Tools - Sign](./scst-policy/migration.hbs.md).
</br></br>

#### <a id="1-3-tbs-deprecations"></a> Tanzu Build Service

- The Ubuntu Bionic stack is deprecated:
Ubuntu Bionic stops receiving support in April 2023.
VMware recommends you migrate builds to Jammy stacks in advance.
For how to migrate builds, see [Use Jammy stacks for a workload](tanzu-build-service/dependencies.md#using-jammy).
- The Cloud Native Buildpack Bill of Materials (CNB BOM) format is deprecated:
It is still activated by default in Tanzu Application Platform v1.3 and v1.4.
VMware plans to deactivate this format by default in Tanzu Application Platform v1.5
and remove support in Tanzu Application Platform v1.6.
To manually deactivate legacy CNB BOM support, see [Deactivate the CNB BOM format](tanzu-build-service/install-tbs.md#deactivate-cnb-bom).
</br></br>

#### <a id="1-3-apps-plugin-deprecations"></a> Tanzu CLI Apps plug-in

- The default value for the `--update-strategy` flag will change from `merge` to `replace` in
  Tanzu Application Platform v1.7.0.
- The `tanzu apps workload update` command is deprecated and marked for removal in Tanzu Application
  Platform 1.5.0. Use `tanzu apps workload apply` instead.
</br></br>
