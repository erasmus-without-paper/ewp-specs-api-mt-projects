Mobility Tool+ Projects API
===========================

* [What is the status of this document?][statuses]
* [See the index of all other EWP Specifications][develhub]


Summary
-------

This document describes the **Mobility Tool+ Projects API**.
It is assumed that this API is implemented by only one host managed by
the Directoriate-General Education and Culture Unit (DG EAC) of the European Commission.
However, the specification itself does not limit the number of hosts.

Once implemented by the host, it allows external clients to retrieve list of projects
for a particular institution and call year.


Request method
--------------

 * Requests MUST be made with either HTTP GET or HTTP POST method. Servers MUST
   support both these methods. Servers SHOULD reject all other request methods.


Request parameters
------------------

Parameters MUST be provided in the regular `application/x-www-form-urlencoded`
format.


### `pic` (required)

A PIC of institution the client wants to retrieve information on.

Clients may retrieve proper PIC from other EWP APIs (most often, the [Registry Service][registry-spec]).

### `call_year` (required)

A call year (integer) of projects being returned.


Security
--------

This version of this API uses [standard EWP Authentication and Security,
Version 2][sec-v2]. Server implementers choose which security methods they
support by declaring them in their Manifest API entry.

This API provides data which is also usually accessible to the anonymous public
by other channels. It is RECOMMENDED for server implementers to not be overly
strict on security methods they require (i.e. it is RECOMMENDED to *not*
require extra layers of encryption in requests and responses - TLS seems more
than enough). Server implementers MAY also consider allowing this API to be
accessed by [anonymous clients][cliauth-none].


Handling of invalid parameters
------------------------------

 * General [error handling rules][error-handling] apply.

 * Invalid (unknown) `pic` MUST result in a HTTP 400 error.
 
 * We assume every positive integer being a valid `call_year`. If the provided `pic` is valid
   and there are no projects for the provided `call_year`, server MUST return a valid (HTTP 200)
   XML response with no `project` elements.


Response
--------

Servers MUST respond with a valid XML document described by the
[response.xsd](response.xsd) schema. See the schema annotations for further
information.


[develhub]: http://developers.erasmuswithoutpaper.eu/
[statuses]: https://github.com/erasmus-without-paper/ewp-specs-management#statuses
[registry-spec]: https://github.com/erasmus-without-paper/ewp-specs-api-registry
[error-handling]: https://github.com/erasmus-without-paper/ewp-specs-architecture#error-handling
[cliauth-none]: https://github.com/erasmus-without-paper/ewp-specs-sec-cliauth-none
