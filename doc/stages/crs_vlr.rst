:orphan:

.. _SRS VLR order:

SRS VLR Order
=============

PDAL supports numerous VLRs containing spatial reference information that may be contained
in a LAS, LAZ or COPC file. The following spatial reference types are supported when found in
a VLR with the proper user ID and record ID::

wkt1 : well-known text version 1 (User ID "LASF_Projection", Record ID 2112)
wkt2 : well-known text version 2 (User ID "LASF_Projection", Record ID 4224)
projjson : PROJ format encoded as JSON (User ID "PDAL", Record ID 4225)
geotiff : Geotiff (User ID "LASF_Projection", Record ID 34735)

The default handling of spatial reference VLRs is as follows:

If a wkt2 VLR is found, it is used. If no WKT2 VLR is found and a projjson VLR is found,
it is used. If no wkt2 or projjson VLR is found, a geotiff or wkt1 VLR will be used
according to the WKT bit of the global encoding field in the LAS header (see the LAS
specification for details).

Both the COPC and LAS readers support an option to override the default behavior.
The option 'srs_vlr_order' can be used to specify the order in which found spatial
reference VLRs should be used. The option supports a comma-separated list of the
values above ('wkt1', 'wkt2', 'projjson' and 'geotiff').
Each value can appear at most once in the list. 'geotiff' is not supported for COPC files.
Values cannot be repeated.

NOTE:
-----
Once a VLR has been found according to the rules above, it is interpreted by the system
as found. Invalid spatial reference specifications don't result in a fallback to
other VLRs that might exist.

