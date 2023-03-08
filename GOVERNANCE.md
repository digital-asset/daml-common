# Governance of daml-common

## Goals

`daml-common` is a set of base scala libraries developed in-house at DA that are meant for wide adoption across all DA products. By selecting a core set of "blessed" libraries we encourage a consistent experience for the development team as well as for the clients using our software. The types of libaries that we envisage will find their home in this repository include but are not limited to:

* logging, metrics, tracing
* resource management
* database access abstractions
* configuration and CLI tooling
* TLS and access token utilities
* self-service error codes
* security evidencing
* functional utilities such as non-empty wrapper

## Process

### Submission
Inclusion of a new library in the `daml-common` repository must be proposed through a GitHub issue. A valid submission should contain
* the name of the library to be included
* a github reference, in case the library already exists in one of the DA repositories
* justification of why this library must be included and why existing libraries do not serve the purpose at the moment
* applicability, i.e. which of the DA projects will benefit from the inclusion
* migration strategy for the existing DA projects
* a list of third party libraries that the new library will bring as a dependency
* build system requirements
* proposed list of the library maintainers that will become code owners on the corresponding directory

### Discussion
The inclusion of a new library is discussed on the GitHub issue. All DA engineering is invited to take part. In order to be considered conclusive a discussion must garner the attention of at least 5 engineers.

### Acceptance
Special role in the process is given to the root code owners of this repository. They assume the role of the arbiters of the discussion surrounding inclusion of the new libraries. It does not mean that they have the autocratic power over the contents of the repository. It rather means that they are the gate keepers of the process that can asses that a sufficient consensus has been reached in the github issue discussion. Think of their role as akin to that shared by the speaker of the house of commons in the UK.

### Seeding
One of the root code owners creates a directory intended to contain the library and adjusts the CODEOWNERS file to list the designated maintainers.

### Development
The library is developed in the `daml-common` repository. This process must include
* providing code with unit tests
* providing documentation in form of a README file as well as documenting the code forming the library interface
* adjusting the release definition to contain the new artifacts
* adjusting the continuous integration to build, test and release the new library
* adjusting the 3rd party library whitelist specifying the required dependencies

The contributions to the libraries are conducted through standard merge PRs. It is the responsibility of the maintainers of the specific library to uphold the required quality standards.

### Proposing changes
Changes to the existing libraries can be suggested by raising an issue. A valid submission should contain
* the name of the library to be modified
* the description of the proposed change
* applicability, i.e. which of the DA projects will benefit from the inclusion
* migration strategy for the existing DA projects

It is the responsibility of the library maintainers to respond to the proposal and to decide whether it is a modification worth pursuing or not.

## Quality

The daml-common repository sets a very high bar on the quality of the libraries included. It should not become a dump of half-baked ideas or where circular dependencies are resolved for lack of a better place. All libraries must
* use standardized build tooling
* use blessed 3rd party dependencies
* be sufficiently tested
* be sufficiently documented
* follow standardized coding format
* adhere to standardized compiler and wart remover flags

## Releasing

* The daml-common repository is not tied to the daml versioning cadence. It follows own semver numbering schema.
* Artifacts will be released to maven. 
* Projects consuming libraries contained in this repository can opt for either using the maven artifacts or for incorporating it as a git submodule.
