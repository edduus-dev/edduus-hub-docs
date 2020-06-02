This is sub-document of Edduus Hub documentation. For the reference, please refer to the [parent document](README.md).

# Organization Module

## Overview

There will be two types of partner organizations in Edduus: Industry Partner, and Education Provider.

An industry partner is any organization that wishes to leverage off the Edduus ecosystem to provide industry specific training pathways consisting of Blocks for existing and potential employees. An example scenario would be Tesla providing “Tesla Automotive Training Program” for potential service technicians.

An education provider on the other hand is an agency who leverages off Edduus to provide education to their constituents. Unlike industry partners, education providers must be able to administer a completely separate and distinct set of students from the Edduus community. That said, in addition to supplying their own blocks, education providers also have the option to employ teachers outside of Edduus. Such agent services are particularly useful when used as a supplemental education program where a mix of physical education and remote education is needed. For example, a technical college would be able to offer on-campus classes for learning how to operate specialized equipment while allowing the students to study other areas at their own pace.

#### Note: This module is in active development, and actual commands may vary.

## Register organization name

Standard fee is 10edtoken

```bash
edcli tx organization register [name] --from [buyer]
```

## Set organization name

```bash
edcli tx organization set-info [name] [description] --from [owner]
```

## Query all registered organization names

```bash
edcli q organization all
```

## Query organization info

```bash
edcli q organization info [name]
```

## Example of usage

```bash
# Register new organization using existing
# Edduus Hub account
edcli tx organization register "Edduus" --from teacher
# Add information to the organization
edcli tx organization set-info Edduus "Education on blockchain" "Worldwide" --from teacher
# Query organization info
edcli q organization info Edduus
# Output:
# {
#   "description": "Education on blockchain",
#   "location": "Worldwide"
# }
```
