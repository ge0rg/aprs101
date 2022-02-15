APRS Specification Recovery Project
===================================

The `APRS protocol specification V1.0 <http://www.aprs.org/doc/APRS101.PDF>`_
only exists in PDF format, the original has been lost.

The goal of this project is to extract as much of the content of the
APRS101.PDF document into a modern markup format that can be used for future
development of the protocol.

The pipeline used to create the RST in this repository was:

1. Convert the PDF into Word using an online converter tool
2. Convert the Word document using `PanDoc <https://pandoc.org/>`_ into RST
3. Remove the PDF document's ToC


To build the HTML version, run the following command:

.. code-block:: sh

    sphinx-build source output
