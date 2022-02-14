   |image0|

==================== ===============================================
**Authors**             The APRS Working Group
==================== ===============================================
**Document Version**    **Approved Version 1.0.1**
**Filename**            aprs101.pdf
**Date of Issue**       **29 August 2000**
**Copyright**           ©2000 APRS Working Group All rights reserved
**Technical Editor**    Ian Wade, G3NRW
==================== ===============================================

..

   APRS Protocol Reference Protocol Version 1.0

   by the APRS Working Group Edited by Ian Wade

   Published by

   Tucson Amateur Packet Radio Corp 8987–309 East Tanque Verde Road,
   #337 Tucson

   AZ 85749-9399

   United States of America
   `http://www.tapr.org <http://www.tapr.org/>`__

   ISBN 0-9644707-6-4

   TAPR Publication Number: 99-4

   Copyright ©2000 APRS Working Group All rights reserved

   APRS\ :sup:`®` is a registered trademark of Bob Bruninga.

   WinAPRS™, MacAPRS™, X-APRS™, PalmAPRS™ and APRS/CE™ are trademarks
   using the APRS\ :sup:`®` name, licensed from Bob Bruninga.

   This document may be copied for non-commercial purposes only, and
   must include the above copyright statement and trademark statements
   in full.

   **FOREWORD**

   This APRS Protocol Reference document represents the coming-of-age of
   WB4APR’s baby. Starting with a simple concept — a way to track the
   location of moving objects via packet radio

   — programs using the APRS protocol have grown into perhaps the most
   popular packet radio application in use today. It’s also become one
   of the most complex; from the simple idea grew, and still grows, a
   tactical communications system of tremendous capability. Like many
   ham projects, the APRS protocol was designed as it was being
   implemented, and many of its intricacies have never been documented.

   Until now. This specification defines the APRS on-air protocol with a
   precision and clarity that make it a model for future efforts. The
   work done by members of the APRS Working Group, as well as Technical
   Editor Ian Wade, G3NRW, should be recognized as a tremendous
   contribution to the packet radio art. With this document available,
   there is now no excuse for any developer to improperly implement the
   APRS protocol.

   As an APRS Working Group member whose role was mainly that of
   observer, I was fascinated with the interplay among the APRS authors
   and the Technical Editor as the specification took form. Putting onto
   paper details that previously existed only in the minds of the
   authors exposed ambiguities, unconsidered consequences, and even
   errors in what the authors thought they knew. The discussion that
   followed each draft, and the questions Ian posed as he tried to wring
   out the uncertainties, gave everyone a better understanding of the
   protocol. I am sure that this process has already contributed to
   better interoperability among existing APRS applications.

   Everyone who has watched the specification develop, from the initial
   mention in April 1999 until release of this Version 1.0 document in
   August 2000, knows that the process took much longer than was hoped.
   At the same time, they saw the draft transformed from a skeleton into
   a hefty book of over 110 pages. With the specification now in hand, I
   think we can all say the wait was worth it. Congratulations to the
   APRS Working Group and, in particular, to G3NRW, for a major
   contribution to the literature of packet radio.

   John Ackermann, N8UR

   TAPR Vice President and APRS Working Group Administrative Chair
   August 2000

APRS PROTOCOL REFERENCE

   **TABLE OF CONTENTS**

`PREAMBLE 1 <#preamble>`__

APRS Working Group 1

Acknowledgements 1

Document Version Number 1

Release History 2

Document Conventions 2

Feedback 2

`AUTHORS’ FOREWORD 3 <#authors-foreword>`__

Disclaimer 3

`THE STRUCTURE OF THIS SPECIFICATION
5 <#the-structure-of-this-specification>`__

1. `INTRODUCTION TO APRS 7 <#introduction-to-aprs>`__

What is APRS? 7

APRS Features 8

2. `THE APRS DESIGN PHILOSOPHY 9 <#the-aprs-design-philosophy>`__

Net Cycle Time 9

Packet Timing 10

Generic Digipeating 11

Communicating Map Views Unambiguously 11

3. `APRS AND AX.25 12 <#aprs-and-ax.25>`__

Protocols 12

The AX.25 Frame 12

4. `APRS DATA IN THE AX.25 DESTINATION AND SOURCE ADDRESS FIELDS
      13 <#aprs-data-in-the-ax.25-destination-and-source-address-fields>`__

The AX.25 Destination Address Field 13

Generic APRS Destination Addresses 13

Generic APRS Address with Symbol 14

APRS Software Version Number 14

Mic-E Encoded Data 15

Maidenhead Grid Locator in Destination Address 15

Alternate Nets 15

Generic APRS Digipeater Path 15

The AX.25 Source Address SSID to specify Symbols 16

5. `APRS DATA IN THE AX.25 INFORMATION FIELD
      17 <#aprs-data-in-the-ax.25-information-field>`__

Generic Data Format 17

APRS Data Type Identifier 17

APRS Data and Data Extension 18

Comment Field 20

Base-91 Notation 20

APRS Data Units 21

6. `TIME AND POSITION FORMATS 22 <#time-and-position-formats>`__

Time Formats 22

Use of Timestamps 23

Latitude Format 23

Longitude Format 23

Position Coordinates 24

Position Ambiguity 24

Default Null Position 25

Maidenhead Locator (Grid Square) 25

NMEA Data 25

Altitude 26

7. `APRS DATA EXTENSIONS 27 <#aprs-data-extensions>`__

Course and Speed 27

Wind Direction and Wind Speed 27

Power, Effective Antenna Height/Gain/ Directivity 28

Range Circle Plot 29

Pre-Calculated Radio Range 29

Omni-DF Signal Strength 29

Bearing and Number/Range/ Quality 30

Area Object Descriptor 31

8. `POSITION AND DF REPORT DATA FORMATS
      32 <#position-and-df-report-data-formats>`__

Position Reports 32

DF Reports 34

9. `COMPRESSED POSITION REPORT DATA FORMATS
      36 <#compressed-position-report-data-formats>`__

The Advantages of Data Compression 36

Compressed Data Format 37

Symbol 37

Lat/Long Encoding 38

Lat/Long Decoding 38

Course/Speed, Pre-Calculated Radio Range and Altitude 38

The Compression Type (T) Byte 39

Altitude 40

New Trackers 40

Old Trackers 41

Compressed Report Formats 41

10. MIC-E DATA FORMAT 42

Mic-E Data Format 42

Mic-E Data Payload 42

Mic-E Destination Address Field 43

Destination Address Field Encoding 43

Mic-E Messages 45

Destination Address SSID Field 46

Mic-E Information Field 46

Information Field Data 46

Longitude Degrees Encoding 47

Longitude Minutes Encoding 48

Longitude Hundredths of Minutes Encoding 49

Speed and Course Encoding 49

SP+28 Encoding 50

DC+28 Encoding 51

SE+28 Encoding 52

Example of Mic-E Speed and Course Encoding 52

Decoding the Speed and Course 52

Example of Decoding the Information Field Data 53

Mic-E Position Ambiguity 53

Mic-E Telemetry Data 54

Mic-E Status Text 54

Maidenhead Locator in the Mic-E Status Text Field 55

Altitude in the Mic-E Status Text Field 55

Mic-E Data in Non-APRS Networks 56

11. OBJECT AND ITEM REPORTS 57

Objects and Items 57

Replacing an Object / Item 57

Killing an Object / Item 57

Object Report Format 58

Item Report Format 59

Area Objects 60

Signpost Objects/Items 61

Obsolete Object Format 61

12. WEATHER REPORTS 62

Weather Report Types 62

Data Type Identifiers 62

Raw Weather Reports 62

Positionless Weather Reports 63

APRS Software Type 63

Weather Unit Type 63

Positionless Weather Data 64

Location of a Raw and Positionless Weather Stations 65

Symbols with Raw and Positionless Weather Stations 65

Complete Weather Reports with Timestamp and Position 65

Storm Data 67

National Weather Service Bulletins 67

13. TELEMETRY DATA 68

Telemetry Report Format 68

On-Air Definition of Telemetry Parameters 68

Parameter Name Message 69

Unit/Label Message 69

Equation Coefficients Message 70

Bit Sense/ Project Name Message 70

14. MESSAGES, BULLETINS AND ANNOUNCEMENTS 71

Messages 71

Message Acknowledgement 72

Message Rejection 72

Multiple Acknowledgements 72

Message Groups 72

General Bulletins 73

Announcements 73

Group Bulletins 74

National Weather Service Bulletins 74

NTS Radiograms 75

Obsolete Bulletin and Announcement Format 75

Bulletin and Announcement Implementation Recommendations 76

15. STATION CAPABILITIES, QUERIES AND RESPONSES 77

Station Capabilities 77

Queries and Responses 77

General Queries 78

Directed Station Queries 79

16. STATUS REPORTS 80

Status Report with Beam Heading and Effective Radiated Power 81

Status Report with Maidenhead Grid Locator 81

Transmitting Status Reports 82

17. NETWORK TUNNELING AND THIRD-PARTY DIGIPEATING 83

Third-Party Networks 83

Source Path Header 83

Third-Party Header 85

Action on Receiving a Third-Party packet 86

An Example of Sending a Message through the Internet 86

18. USER-DEFINED DATA FORMAT 87

19. OTHER PACKETS 89

Invalid Data or Test Data Packets 89

All Other Packets 89

20. APRS SYMBOLS 90

Three Methods 90

The Symbol Tables 90

Symbols in the AX.25 Information Field 90

Overlays with Symbols in the AX.25 Information Field 91

Symbols in the AX.25 Destination Address 92

Overlays with Symbols in the AX.25 Destination Address 92

Symbol in the Source Address SSID 93

Symbol Precedence 93

APPENDICES

APPENDIX 1: APRS DATA FORMATS 94

APPENDIX 2: THE APRS SYMBOL TABLES 104

APPENDIX 3: 7-BIT ASCII CODE TABLE 107

APPENDIX 4: DECIMAL-TO-HEX CONVERSION TABLE 109

APPENDIX 5: GLOSSARY 110

Units Conversion Table 114

Fahrenheit / Celsius Temperature Conversion Equations 114

APPENDIX 6: REFERENCES 115

APPENDIX 7: DOCUMENT RELEASE HISTORY 116

   **Preamble** 1

PREAMBLE
========

   **APRS Working**

**Group**

   The APRS Working Group is an unincorporated association whose members
   undertake to further the use and enhance the value of the APRS
   protocols by

a. publishing and maintaining a formal APRS Protocol Specification; (b)
      publishing validation tests and other tools to enable compliance
      with the Specification; (c) supporting an APRS Certification
      program; and (d) generally working to improve the capabilities of
      APRS within the amateur radio community.

..

   Although the Working Group may receive support from TAPR and other
   organizations, it is an independent body and is not affiliated with
   any organization. The Group has no budget, collects no dues, and owns
   no assets.

   The current members of the APRS Working Group are:

   John Ackermann, N8UR Administrative Chair & TAPR Representative Bob
   Bruninga, WB4APR Technical Chair, founder of APRS

   Brent Hildebrand, KH2Z Author of APRS+SA Stan Horzepa, WA1LOU
   Secretary

   Mike Musick, N0QBF Author of pocketAPRS

   Keith Sproul, WU2Z Co-Author of WinAPRS/MacAPRS/X-APRS Mark Sproul,
   KB2ICI Co-Author of WinAPRS/MacAPRS/X-APRS

   **Acknowledgements** This document is the result of contributions
   from many people. It includes much of the material produced by
   individual members of the Working Group.

   In addition, the paper on the Mic-E data format by Alan Crosswell,
   N2YGK, and Ron Parsons, W5RKN was a useful starting point for
   explaining the complications of this format.

   **Document Version Number**

   Except for the very first public draft release of the APRS Protocol
   Reference, the document version number is a 3-part number “P.p.D”
   (for an approved document release) or a 4-part number “P.p.Dd” (for a
   draft release):

============================== ======================= ============ ====
   **Document Version Number**                                      
============================== ======================= ============ ====
   **APRS Protocol Version**      **Document Release**    **Draft** 
   **Major Release**              **Minor Release**                 
   P.                             p.                      D            d
============================== ======================= ============ ====

..

   Thus, for example:

-  Document version number “1.2.3” refers to document release 3 covering
      APRS Protocol Version 1.2.

-  Document version number “1.2.3c” is draft “c” of that document.

..

   **Release History** The release history for this document is listed
   in Appendix 7.

   **Document Conventions**

   This document uses the following conventions:

-  Courier font ASCII characters in APRS data.

-  ␣ ASCII space character.

-  … (ellipsis) zero or more characters.

-  /$ Symbol from Primary Symbol Table.

-  \\$ Symbol from Alternate Symbol Table.

-  0x hexadecimal (e.g. 0x1d).

-  All callsigns are assumed to have SSID –0 unless otherwise specified.

-  **Yellow marker** (appears as light gray background in hard copy).
      Marks text of interest — especially useful for highlighting single
      literal ASCII characters (e.g. **"**) where they appear in APRS
      data.

-  Shaded areas in packet format diagrams are optional fields.

..

   **Feedback** Please address your feedback or other comments regarding
   this document to the TAPR *aprsspec* mail list.

   To join the list, start at
   `http://www.tapr.org <http://www.tapr.org/>`__ and then follow the
   path Special Interest Groups  APRS Specification  Join APRS Spec
   Discussion List.

AUTHORS’ FOREWORD
=================

   This reference document describes what is known as *APRS Protocol
   Version 1.0*, and is essentially a description of how APRS operates
   today.

   It is intended primarily for the programmer who wishes to develop
   APRS- compliant applications, but will also be of interest to the
   ordinary user who wants to know more about what goes on “under the
   hood”.

   It is not intended, however, to be a dry-as-dust, pedantic, RFC-style
   programming specification, to be read and understood only by the Mr
   Spocks of this world. We have included many items of general
   information which, although strictly not part of the formal protocol
   description, provide a useful background on how APRS is actually used
   on the air, and how it is implemented in APRS software. We hope this
   will put APRS into perspective, will make the document more readable,
   and will not offend the purists too much.

   It is important to realize how APRS originated, and to understand the
   design philosophy behind it. In particular, we feel strongly that
   APRS is, and should remain, a light-weight tactical system — almost
   anyone should be able to use it in temporary situations (such as
   emergencies or mobile work or weather watching) with the minimum of
   training and equipment.

   This document is the result of inputs from many people, and collated
   and massaged by the APRS Working Group. Our sincere thanks go to
   everyone who has contributed in putting it together and getting it
   onto the street. If you discover any errors or omissions or
   misleading statements, please let us know

   — the best way to do this is via the TAPR *aprsspec* mailing list at
   `www.tapr.org. <http://www.tapr.org/>`__

   Finally, users throughout the world are continually coming up with
   new ideas and suggestions for extending and improving APRS. We
   welcome them.

   Again, the best way to discuss these is via the *aprsspec* list.

   The APRS Working Group August 2000

   **Disclaimer** Like any navigation system, APRS is not infallible. No
   one should rely blindly on APRS for navigation, or in life-and-death
   situations. Similarly, this specification is not infallible.

   The members of the APRS Working Group have done their best to define
   the APRS protocol, but this protocol description may contain errors,
   or there may be omissions. It is very likely that not all APRS
   implementations will fully or correctly implement this specification,
   either today or in the future.

   We urge anyone using or writing a program that implements this
   specification to exercise caution and good judgement. The APRS
   Working Group and the specification’s Editor disclaim all liability
   for injury to persons or property that may result from the use of
   this specification or software implementing it.

THE STRUCTURE OF THIS SPECIFICATION
===================================

   This specification describes the overall requirements for developing
   software that complies with APRS Protocol Version 1.0. The
   information flow starts with the standard AX.25 UI-frame, and
   progresses downwards into more and more detail as the use of each
   field in the frame is explored.

   A key feature of the specification is the inclusion of dozens of
   detailed examples of typical APRS packets and related math
   computations.

   Here is an outline of the chapters:

   **Introduction to APRS** — A brief background to APRS and a summary
   of its main features.

   **The APRS Design Philosophy** — The fundamentals of APRS,
   highlighting its use as a real-time tactical communications tool, the
   timing of APRS transmissions and the use of generic digipeating.

   **APRS and AX.25** — A brief refresher on the structure of the AX.25

   UI-frame, with particular reference to the special ways in which APRS
   uses the Destination and Source Address fields and the Information
   field.

   **APRS Data in the AX.25 Destination and Source Address Fields** —
   Details of generic APRS callsigns and callsigns that specify display
   symbols and APRS software version numbers. Also a summary of how
   Mic-E encoded data is stored in the Destination Address field, and
   how the Source Address SSID can specify a display icon.

   **APRS Data in the AX.25 Information Field** — Details of the
   principal constituents of APRS data that are stored in the
   Information field. Contains the APRS Data Type Identifiers table, and
   a summary of all the different types of data that the Information
   field can hold.

   **Time and Position Formats** — Information on formats for
   timestamps, latitude, longitude, position ambiguity, Maidenhead
   locators, NMEA data and altitude.

   **APRS Data Extensions** — Details of optional data extensions for
   station course/speed, wind speed/direction, power/height/gain,
   pre-calculated radio range, DF signal strength and Area Object
   descriptor.

   **Position and DF Report Data Formats** — Full details of these
   report formats.

   **Compressed Position Report Data Formats** — Full details of how
   station position and APRS data extensions are compressed into very
   short packets.

   **Mic-E Data Format** —Mic-E encoding of station lat/long position,
   altitude, course, speed, Mic-E message code, telemetry data and APRS
   digipeater path into the AX.25 Destination Address and Information
   fields.

   **Object and Item Reports** — Full information on how to set up APRS
   Objects and Items, and details of the encoding of Area Objects
   (circles, lines, ellipses etc).

   **Weather Reports** — Full format details for weather reports from
   stand- alone (positionless) weather stations and for reports
   containing position information. Also details of storm data format.

   **Telemetry Data** — A description of the MIM/KPC-3+ telemetry data
   format, with supporting information on how to tailor the
   interpretation of the raw data to individual circumstances.

   **Messages, Bulletins and Announcements** — Full format information.

   **Station Capabilities, Queries and Responses** — Details of the ten
   different types of query and expected responses.

   **Status Reports** — The format of general status messages, plus the
   special cases of using a status report to contain meteor scatter beam
   heading/power and Maidenhead locator.

   **Network Tunneling** — The use of the Source Path Header to allow
   tunneling of APRS packets through third-party networks that do not
   understand AX.25 addresses, and the use of the third-party Data Type
   Identifier.

   **User-Defined Data Format** — APRS allows users to define their own
   data formats for special purposes. This chapter describes how to do
   this.

   **Other Packets** — A general statement on how APRS is to handle any
   other packet types that are not covered by this specification.

   **APRS Symbols** —How to specify APRS symbols and symbol overlays, in
   position reports and in generic GPS destination callsigns.

   **APRS Data Formats** — An appendix containing all the APRS data
   formats collected together for easy reference.

   **The APRS Symbol Tables** —A complete listing of all the symbols in
   the Primary and Alternate Symbol Tables.

   **ASCII Code Table** — The full ASCII code, including decimal and hex
   codes for each character (the decimal code is needed for compressed
   lat/long and altitude computations), together with the hex codes for
   bit-shifted ASCII characters in AX.25 addresses (useful for Mic-E
   decoding and general on-air packet monitoring).

   **Glossary** — A handy one-stop reference for the many APRS-specific
   terms used in this specification.

   **References** — Pointers to other documents that are relevant to
   this specification.

INTRODUCTION TO APRS
====================

   **What is APRS?** APRS is short for *Automatic Position Reporting
   System*, which was designed by Bob Bruninga, WB4APR, and introduced
   by him at the 1992 TAPR/ ARRL Digital Communications Conference.

   Fundamentally, APRS is a packet communications protocol for
   disseminating live data to everyone on a network in real time. Its
   most visual feature is the combination of packet radio with the
   Global Positioning System (GPS) satellite network, enabling radio
   amateurs to automatically display the positions of radio stations and
   other objects on maps on a PC. Other features not directly related to
   position reporting are supported, such as weather station reporting,
   direction finding and messaging.

   APRS is different from regular packet in several ways:

-  It provides maps and other data displays, for vehicle/personnel
      location and weather reporting in real time.

-  It performs all communications using a one-to-many protocol, so that
      everyone is updated immediately.

-  It uses generic digipeating, with well-known callsign aliases, so
      that prior knowledge of network topology is not required.

-  It supports intelligent digipeating, with callsign substitution to
      reduce network flooding.

-  Using AX.25 UI-frames, it supports two-way messaging and distribution
      of bulletins and announcements, leading to fast dissemination of
      text information.

-  It supports communications with the Kenwood TH-D7 and TM-D700 radios,
      which have built-in TNC and APRS firmware.

..

   Conventional packet radio is really only useful for passing bulk
   message traffic from point to point, and has traditionally been
   difficult to apply to real-time events where information has a very
   short lifetime. APRS turns packet radio into a real-time tactical
   communications and display system for emergencies and public service
   applications.

   APRS provides universal connectivity to all stations, but avoids the
   complexity, time delays and limitations of a connected network. It
   permits any number of stations to exchange data just like voice users
   would on a voice net. Any station that has information to contribute
   simply sends it, and all stations receive it and log it.

   APRS recognizes that one of the greatest real-time needs at any
   special event or emergency is the tracking of key assets. Where is
   the marathon leader?

   Where are the emergency vehicles? What’s the weather at various
   points in the county? Where are the power lines down? Where is the
   head of the

   parade? Where is the mobile ATV camera? Where is the storm?

   To address these questions, APRS provides a fully featured automatic
   vehicle location and status reporting system. It can be used over any
   two-way radio system including amateur radio, marine band, and
   cellular phone. There is even an international live APRS tracking
   network on the Internet.

**APRS**

   **Features**

   APRS runs on most platforms, including DOS, Windows 3.x, Windows
   95/98, MacOS, Linux and Palm. Most implementations on these platforms
   support the main features of APRS:

-  **Maps** — APRS station positions can be plotted in real-time on
      maps, with coverage from a few hundred yards to worldwide.
      Stations reporting a course and speed are dead-reckoned to their
      present position. Overlay databases of the locations of APRS
      digipeaters, US National Weather Service sites and even amateur
      radio stores are available. It is possible to zoom in to any point
      on the globe.

-  **Weather Station Reporting** — APRS supports the automatic display
      of remote weather station information on the screen.

-  **DX Cluster Reporting** — APRS an ideal tool for the DX cluster
      user. Small numbers of APRS stations connected to DX clusters can
      relay DX station information to many other stations in the local
      area, reducing overall packet load on the clusters.

-  **Internet Access** — The Internet can be used transparently to
      cross-link local radio nets anywhere on the globe. It is possible
      to telnet into Internet APRS servers and see hundreds of stations
      from all over the world live. Everyone connected can feed their
      locally heard packets into the APRS server system and everyone
      everywhere can see them.

-  **Messages** — Messages are two-way messages with acknowledgement.
      All incoming messages alert the user on arrival and are held on
      the message screen until killed.

-  **Bulletins and Announcements** —Bulletins and announcements are
      addressed to everyone. Bulletins are sent a few times an hour for
      a few hours, and announcements less frequently but possibly over a
      few days.

-  **Fixed Station Tracking** — In addition to automatically tracking
      mobile GPS/LORAN-equipped stations, APRS also tracks from manual
      reports or grid squares.

-  **Objects** — Any user can place an APRS Object on his own map, and
      within seconds that object appears on all other station displays.
      This is particularly useful for tracking assets or people that are
      not equipped with trackers. Only one packet operator needs to know
      where things are (e.g. by monitoring voice traffic), and as he
      maintains the positions and movements of assets on his screen, all
      other stations running APRS will display the same information.

THE APRS DESIGN PHILOSOPHY
==========================

   **Net Cycle Time** It is important to note that APRS is primarily a
   *real-time, tactical* communications tool, to help the flow of
   information for things like special events, emergencies, Skywarn, the
   Emergency Operations Center and just plain in-the-field use under
   stress. But like the real world, for 99% of the time it is operating
   routinely, waiting for the unlikely serious event to happen.

   Anything which is done to enhance APRS must not undermine its ability
   to operate in local areas under stress. Here are the details of that
   philosophy:

1. APRS uses the concept of a “net cycle time”. This is the time within
      which a user should be able to hear (at least once) all APRS
      stations within range, to obtain a more or less complete picture
      of APRS activity. The net cycle time will vary according to local
      conditions and with the number of digipeaters through which APRS
      data travels.

2. The objective is to have a net cycle time of 10 minutes for local
      use. This means that within 10 minutes of arrival on the scene, it
      is possible to captured the entire tactical picture.

3. All stations, even fixed stations, should beacon their position at
      the net cycle time rate. In a stress situation, stations are
      coming and going all the time. The position reports show not only
      where stations are without asking, but also that they are still
      active.

4. It is not reasonable to assume that all APRS users responding to a
      stress event understand the ramifications of APRS and the
      statistics of the channel — user settings cannot be relied on to
      avoid killing a stressed net. Thus, to try to anticipate when the
      channel is under stress, APRS automatically adjusts its net cycle
      time according to the number of digipeaters in the UNPROTO path:

   -  Direct operation (no digipeaters): 10 minutes (probably an event).

   -  Via one digipeater hop: 10 minutes (probably an event).

   -  Via two digipeater hops: 20 minutes.

   -  Via three or more digipeater hops: 30 minutes.

5. Since almost all home stations set their paths to three or more
      digipeaters, the default net cycle time for routine daily
      operation is 30 minutes. This should be a universal standard that
      everyone can bank on

..

   — if you routinely turn on your radio and APRS and do nothing else,
   then in 30 minutes you should have virtually the total picture of all
   APRS stations within range.

6. Since knowing where the digipeaters are located is fundamental to
      APRS

..

   connectivity, digipeaters should use multiple beacon commands to
   transmit position reports at different rates over different paths;
   i.e. every 10 minutes for sending position reports locally, and every
   30 minutes for sending them via three digipeaters (plus others rates
   and distances as needed).

7. If the net cycle time is too long, users will be tempted to send
      queries for APRS stations. This will increase the traffic on the
      channel unnecessarily. Thus the recommended extremes for net cycle
      time are 10 and 30 minutes — this gives network designers the
      fundamental assumptions for channel loading necessary for good
      engineering design.

..

   **Packet Timing** Since APRS packets are error-free, but are not
   guaranteed delivery, APRS transmits information redundantly. To
   assure rapid delivery of new or changing data, and to preserve
   channel capacity by reducing interference from old data, APRS should
   transmit new information more frequently than old information.

   There are several algorithms in use to achieve this:

-  **Decay Algorithm** — Transmit a new packet once and n seconds later.
      Double the value of n for each new transmission. When n reaches
      the net cycle time, continue at that rate. Other factors besides
      “doubling” may be appropriate, such as for new message lines.

-  **Fixed Rate** — Transmit a new packet once and n seconds later.
      Transmit it x times and stop.

-  **Message-on-Heard** — Transmit a *new* packet according to either
      algorithm above. If the packet is still valid, and has not been
      acknowledged, and the net cycle time has been reached, then the
      recipient is probably not available. However, if a packet is then
      subsequently heard from the recipient, try once again to transmit
      the packet.

-  **Time-Out** — This term is used to describe a time period beyond
      which it is reasonable to assume that a station no longer exists
      or is off the air if no packets have been heard from it. A period
      of 2 hours is suggested as the nominal default timeout. This
      time-out is not used in any transmitting algorithms, but is useful
      in some programs to decide when to cease displaying stations as
      “active”. Note that on HF, signals come and go, so decisions about
      activity may need to be more flexible.

..

   **Generic Digipeating** The power of APRS in the field derives from
   the use of *generic* digipeating, in that packets are propagated
   without a priori knowledge of the network.

   There are six powerful techniques which have evolved since APRS was
   introduced in 1992:

1. **RELAY** — Every VHF APRS TNC is assumed to have an alias of

..

   RELAY, so that anyone can use it as a digipeater at any time.

2. **ECHO** — HF stations use the alias of ECHO as an alternative to
      RELAY. (However, bearing in mind the nature of HF propagation,
      this has the potential of causing interference over a wide area,
      and should only be used sparingly by mobile stations).

3. **WIDE** — Every high-site digipeater is assumed to have an alias of
      WIDE

..

   for longer distance communications.

4. **TRACE** — Every high-site digipeater that is using callsign
      substitution is assumed to have the alias of TRACE. These
      digipeaters self-identify packets they digipeat by inserting their
      own call in place of RELAY, WIDE or TRACE.

5. **WIDEn-N** — A digipeater that supports WIDEn-N digipeating will
      digipeat any WIDEn-N packet that is “new” and will subtract 1 from
      the SSID until the SSID reaches –0. The digipeater keeps a copy or
      a checksum of the packet and will not digipeat that packet again
      within (typically) 28 seconds. This considerably reduces the
      number of superfluous digipeats in areas with many digipeaters in
      radio range of each other.

6. **GATE** — This generic callsign is used by HF-to-VHF Gateway
      digipeaters. Any packet heard on HF via GATE will be digipeated
      locally on VHF. This permits local networks to keep an eye on the
      national and international picture.

**Communicating**

   **Map Views Unambiguously**

   APRS is a tactical geographical system. To maximize its operational
   effectiveness and minimize confusion between operators of different
   systems, users need to have an unambiguous way to communicate to
   others the “location” and “size” (or area of coverage) of any map
   view.

   The APRS convention is by reference to a *center* and *range* which
   specify the geographical center and approximate radius of a circle
   that will fit in the map view independent of aspect ratio. The radius
   of the circle (in nautical miles, statute miles or km) is known as
   the “range scale”. This convention gives all users a simple common
   basis for describing any specific map view to others over any
   communications medium or program.

APRS AND AX.25
==============

   **Protocols** At the link level, APRS uses the AX.25 protocol, as
   defined in *Amateur Packet-Radio Link-Layer Protocol* (see Appendix 6
   for details), utilizing Unnumbered Information (UI) frames
   exclusively. This means that APRS runs in *connectionless* mode,
   whereby AX.25 frames are transmitted without expecting any response,
   and reception at the other end is not guaranteed.

   At a higher level, APRS supports a messaging protocol that allows
   users to send short messages (one line of text) to nominated
   stations, and expects to receive acknowledgements from those
   stations.

   **The AX.25 Frame** All APRS transmissions use AX.25 UI-frames, with
   9 fields of data:

   Bytes:

-  **Flag** — The flag field at each end of the frame is the bit
      sequence 0x7e that separates each frame.

-  **Destination Address** — This field can contain an APRS destination
      callsign or APRS data. APRS data is encoded to ensure that the
      field conforms to the standard AX.25 callsign format (i.e. 6
      alphanumeric characters plus SSID). If the SSID is non-zero, it
      specifies a generic APRS digipeater path.

-  **Source Address** — This field contains the callsign and SSID of the
      transmitting station. In some cases, if the SSID is non-zero, the
      SSID may specify an APRS display Symbol Code.

-  **Digipeater Addresses** — From zero to 8 digipeater callsigns may be
      included in this field. **Note**: These digipeater addresses may
      be overridden by a generic APRS digipeater path (specified in the
      Destination Address SSID).

-  **Control Field** — This field is set to 0x03 (UI-frame).

-  **Protocol ID** — This field is set to 0xf0 (no layer 3 protocol).

-  **Information Field** — This field contains more APRS data. The first
      character of this field is the APRS Data Type Identifier that
      specifies the nature of the data that follows.

-  **Frame Check Sequence** — The FCS is a sequence of 16 bits used for
      checking the integrity of a received frame.

APRS DATA IN THE AX.25 DESTINATION AND SOURCE ADDRESS FIELDS
============================================================

   **The AX.25**

   **Destination Address Field**

   The AX.25 Destination Address field can contain 6 different types of
   APRS information:

-  A generic APRS address.

-  A generic APRS address with a symbol.

-  An APRS software version number.

-  Mic-E encoded data.

-  A Maidenhead Grid Locator (obsolete).

-  An Alternate Net (ALTNET) address.

..

   In all of these cases, the Destination Address SSID may specify a
   generic APRS digipeater path.

   **Generic APRS Destination Addresses**

   APRS uses the following generic beacon-style destination addresses:

+-----------+-----------+-----------+-----------+-----------+---+
|    **     |    **     |    *      |           |    *      |   |
| AIR**\ \* | ALL**\ \* | *AP**\ \* |  **BEACON | *DF**\ \* |   |
|    †      |    **DR   |    *      |           |    **M    |   |
|    **D    | ILL**\ \* | *DX**\ \* |  CQ**\ \* | ICE**\ \* |   |
| GPS**\ \* |    **     |    **R    |    **     |    **     |   |
|    **     | QTH**\ \* | TCM**\ \* | GPS**\ \* | SYM**\ \* |   |
| QST**\ \* |           |           |    *      |           |   |
|           |           |           | *ID**\ \* |           |   |
|           |           |           |    **J    |           |   |
|           |           |           | AVA**\ \* |           |   |
|           |           |           |    **M    |           |   |
|           |           |           | AIL**\ \* |           |   |
|           |           |           |    **     |           |   |
|           |           |           | SKY**\ \* |           |   |
|           |           |           |    **SP   |           |   |
|           |           |           | ACE**\ \* |           |   |
|           |           |           |    **     |           |   |
|           |           |           | SPC**\ \* |           |   |
+===========+===========+===========+===========+===========+===+
|    **     |    **T    |    **     |    *      |    **     |   |
| TEL**\ \* | EST**\ \* | TLM**\ \* | *WX**\ \* | ZIP**\ \* |   |
|           |           |           |           |    †      |   |
+-----------+-----------+-----------+-----------+-----------+---+

..

   The asterisk is a wildcard, allowing the address to be extended (up
   to a total of 6 alphanumeric characters). Thus, for example, WX1,
   WX12 and WX12CD are all valid APRS destination addresses.

   † The **AIR**\ \* and **ZIP**\ \* addresses are being phased out, but
   are needed at present for backward compatibility.

   All of these addresses have an SSID of –0. Non-zero SSIDs are
   reserved for generic APRS digipeating.

   These addresses are copied by everyone. All APRS software must accept
   packets with these destination addresses.

   The address **GPS** (i.e. the 3-letter address **GPS**, not
   **GPS\***) is specifically intended for use by trackers sending
   lat/long positions via digipeaters which have the capability of
   converting positions to compressed data format.

   The addresses **DGPS** and **RTCM** are used by differential GPS
   correction stations. Most software will not make use of packets using
   this address, other than to pass them on to an attached GPS unit.

   The address **SKY** is used for Skywarn stations.

   Packets addressed to **SPCL** are intended for special events. APRS
   software can display such packets to the exclusion of all others, to
   minimize clutter on

   the screen from other stations not involved in the special event. The
   addresses **TEL** and **TLM** is used for telemetry stations.

   **Generic APRS Address with**

**Symbol**

   APRS uses several of the above-listed generic addresses in a special
   way, to specify not only an address but also a display symbol. These
   special addresses are GPSxyz, GPSCnn, GPSEnn, SPCxyz and SYMxyz, and
   are intended for use where it is not possible to include the symbol
   in the AX.25 Information field.

   The GPS addresses above are for general use.

   The SPC addresses are intended for special events. The SYM addresses
   are reserved for future use.

   The characters xy and nn refer to entries in the APRS Symbol Tables.
   The character z specifies a symbol overlay. See Chapter 20: APRS
   Symbols and Appendix 2 for more information.

   **APRS Software Version Number**

   The AX.25 Destination Address field can contain the version number of
   the APRS software that is running at the station. Knowledge of the
   version number can be useful when debugging.

   The following software version types are reserved (xx and xxx
   indicate a version number):

   **APC**\ xxx APRS/CE, Windows CE

   **APD**\ xxx Linux aprsd server

   **APE**\ xxx PIC-Encoder

   **API**\ xxx Icom radios (future)

   **APIC**\ xx ICQ messaging

   **APK**\ xxx Kenwood radios

   **APM**\ xxx MacAPRS

   **APP**\ xxx pocketAPRS

   **APR**\ xxx APRSdos

   **APRS** older versions of APRSdos

   **APRSM** older versions of MacAPRS

   **APRSW** older versions of WinAPRS

   **APS**\ xxx APRS+SA

   **APW**\ xxx WinAPRS

   **APX**\ xxx X-APRS

   **APY**\ xxx Yaesu radios (future)

   **APZ**\ xxx Experimental

   This table will be added to by the APRS Working Group.

   For example, a station using version 3.2.6 of MacAPRS could use the

   destination callsign APM326.

   The Experimental destination is designated for *temporary* use only
   while a product is being developed, before a special APRS Software
   Version address is assigned to it.

**Mic-E Encoded**

**Data**

   Another alternative use of the AX.25 Destination Address field is to
   contain Mic-E encoded data. This data includes:

-  The latitude of the station.

-  A West/East Indicator and a Longitude Offset Indicator (used in
      longitude computations).

-  A Message Code.

-  The APRS digipeater path.

..

   This data is used with associated data in the AX.25 Information field
   to provide a complete Position Report and other information about the
   station (see Chapter 10: Mic-E Data Format).

**Maidenhead Grid**

   **Locator in Destination Address**

   The AX.25 Destination Address field may contain a 6-character
   Maidenhead Grid Locator. For example: **IO91SX**. This format is
   typically used by meteor scatter and satellite operators who need to
   keep packets as short as possible.

   This format is now obsolete.

   **Alternate Nets** Any other destination address not included in the
   specific generic list or the other categories mentioned above may be
   used in Alternate Nets (ALTNETs) by groups of individuals for special
   purposes. Thus they can use the APRS infrastructure for a variety of
   experiments without cluttering up the maps and lists of other APRS
   stations. Only stations using the same ALTNET address should see
   their data.

   **Generic APRS Digipeater Path**

   The SSID in the Destination Address field of all packets is coded to
   specify the APRS digipeater path.

   If the Destination Address SSID is –0, the packet follows the
   standard AX.25 digipeater (“VIA”) path contained in the Digipeater
   Addresses field of the AX.25 frame.

   If the Destination Address SSID is non-zero, the packet follows one
   of 15 generic APRS digipeater paths.

   The SSID field in the Destination Address (i.e. in the 7th address
   byte) is encoded as follows:

   **APRS Digipeater Paths in Destination Address SSID**

   **The AX.25 Source Address SSID to specify Symbols**

   The AX.25 Source Address field contains the callsign and SSID of the
   originating station. If the SSID is –0, APRS does not treat it in any
   special way.

   If, however, the Source Address SSID is non-zero, APRS interprets it
   as a display icon. This is intended for use only with stand-alone
   trackers where there is no other method of specifying a display
   symbol or a destination address (e.g. MIM trackers or NMEA trackers).

   For more information, see Chapter 20: APRS Symbols.

APRS DATA IN THE AX.25 INFORMATION FIELD
========================================

**Generic Data**

**Format**

Bytes:

   **APRS Data Type**

**Identifier**

   In general, the AX.25 Information field can contain some or all of
   the following information:

-  APRS Data Type Identifier

-  APRS Data

-  APRS Data Extension

-  Comment

+----------------+----------------+----------------+----------------+
|    **Generic   |                |                |                |
|    APRS        |                |                |                |
|    Information |                |                |                |
|    Field**     |                |                |                |
+================+================+================+================+
|    **Data Type |    **APRS      |    **APRS Data |    **Comment** |
|    ID**        |    Data**      |    Extension** |                |
+----------------+----------------+----------------+----------------+
|    1           |    n           |    7           |    n           |
+----------------+----------------+----------------+----------------+

..

   Every APRS packet contains an APRS Data Type Identifier (DTI). This
   determines the format of the remainder of the data in the Information
   field, as follows:

   **APRS Data Type Identifiers**

   **Note:** There is one exception to the requirement for the Data Type
   Identifier to be the *first* character in the Information field —
   this is the *Position without Timestamp* (indicated by the **!**
   DTI). The **!** character may occur *anywhere up to and including the
   40th character position* in the Information field. This variability
   is required to support X1J TNC digipeaters which have a string of
   unmodifiable text at the beginning of the field.

   **Note**: The Kenwood TM-D700 radio uses the **'** DTI for *current*
   Mic-E data. The radio does not use the ‘ DTI.

   **APRS Data and Data Extension**

   There are 10 main types of APRS Data:

-  Position

-  Direction Finding

-  Objects and Items

-  Weather

-  Telemetry

-  Messages, Bulletins and Announcements

-  Queries

-  Responses

-  Status

-  Other

..

   Some of this data may also have an APRS Data Extension that provides
   additional information.

   The APRS Data and optional Data Extension follow the Data Type
   Identifier.

   The table on the next page shows a complete list of all the different
   possible types of APRS Data and APRS Data Extension.

+----------------------+----------------------+----------------------+
|                      |    **Possible APRS   |    **Possible APRS   |
|                      |    Data**            |    Data Extension**  |
+======================+======================+======================+
| **Position**         |    Time (DHM or HMS) |    Course and Speed  |
|                      |    Lat/long          |                      |
|                      |    coordinates       |    Power, Effective  |
|                      |                      |    Antenna           |
|                      |    Compressed        |    Hei               |
|                      |    lat/lon           | ght/Gain/Directivity |
|                      | g/course/speed/radio |    Pre-Calculated    |
|                      |    range/altitude    |    Radio Range       |
|                      |    Symbol Table ID   |                      |
|                      |    and Symbol Code   |    Omni DF Signal    |
|                      |                      |    Strength Storm    |
|                      |    Mic-E longitude,  |    Data (in Comment  |
|                      |    speed and course, |    field)            |
|                      |    telemetry or      |                      |
|                      |    status Raw GPS    |                      |
|                      |    NMEA sentence     |                      |
|                      |                      |                      |
|                      |    Raw weather       |                      |
|                      |    station data      |                      |
+----------------------+----------------------+----------------------+
| **Direction          |    Time (DHM or HMS) |    Course and Speed  |
| Finding**            |    Lat/long          |                      |
|                      |    coordinates       |    Power, Effective  |
|                      |                      |    Antenna           |
|                      |    Compressed        |    Hei               |
|                      |    lat/lon           | ght/Gain/Directivity |
|                      | g/course/speed/radio |    Pre-Calculated    |
|                      |    range/altitude    |    Radio Range       |
|                      |    Symbol Table ID   |                      |
|                      |    and Symbol Code   |    Omni DF Signal    |
|                      |                      |    Strength          |
|                      |                      |                      |
|                      |                      |    Bearing and       |
|                      |                      |                      |
|                      |                      | Number/Range/Quality |
|                      |                      |    (in Comment       |
|                      |                      |    field)            |
+----------------------+----------------------+----------------------+
|                      |    Object name       |    Course and Speed  |
+----------------------+----------------------+----------------------+
|                      |    Item name         |    Power, Effective  |
|                      |                      |    Antenna           |
|                      |                      |    Hei               |
|                      |                      | ght/Gain/Directivity |
+----------------------+----------------------+----------------------+
| **Objects and**      |    Time (DHM or HMS) |    Pre-Calculated    |
|                      |    Lat/long          |    Radio Range Omni  |
| **Items**            |    coordinates       |    DF Signal         |
|                      |                      |    Strength Area     |
|                      |    Compressed        |    Object            |
|                      |    lat/lon           |                      |
|                      | g/course/speed/radio |                      |
|                      |    range/altitude    |                      |
+----------------------+----------------------+----------------------+
|                      |    Symbol Table ID   |    Storm Data (in    |
|                      |    and Symbol Code   |    Comment field)    |
+----------------------+----------------------+----------------------+
|                      |    Raw weather       |                      |
|                      |    station data      |                      |
+----------------------+----------------------+----------------------+
| **Weather**          |    Time (MDHM)       |    Wind Direction    |
|                      |    Lat/long          |    and Speed Storm   |
|                      |    coordinates       |    Data (in Comment  |
|                      |                      |    field)            |
|                      |    Compressed        |                      |
|                      |    lat/lon           |                      |
|                      | g/course/speed/radio |                      |
|                      |    range/altitude    |                      |
|                      |    Symbol Table ID   |                      |
|                      |    and Symbol Code   |                      |
|                      |                      |                      |
|                      |    Raw weather       |                      |
|                      |    station data      |                      |
+----------------------+----------------------+----------------------+
| **Telemetry**        |    Telemetry (non    |                      |
|                      |    Mic-E)            |                      |
+----------------------+----------------------+----------------------+
|                      |    Addressee         |                      |
+----------------------+----------------------+----------------------+
|    **Messages,       |    Message Text      |                      |
|    Bulletins and     |    Message           |                      |
|    Announcements**   |    Identifier        |                      |
|                      |                      |                      |
|                      |    Message           |                      |
|                      |    Acknowledgement   |                      |
|                      |    Bulletin ID,      |                      |
|                      |    Announcement ID   |                      |
+----------------------+----------------------+----------------------+
|                      |    Group Bulletin ID |                      |
+----------------------+----------------------+----------------------+
| **Queries**          |    Query Type        |                      |
|                      |                      |                      |
|                      |    Query Target      |                      |
|                      |    Footprint         |                      |
|                      |    Addressee         |                      |
|                      |    (Directed Query)  |                      |
+----------------------+----------------------+----------------------+
|                      |    Position          |    Course and Speed  |
+----------------------+----------------------+----------------------+
|                      |    Object/Item       |    Power, Effective  |
|                      |                      |    Antenna           |
|                      |                      |    Hei               |
|                      |                      | ght/Gain/Directivity |
+----------------------+----------------------+----------------------+
|                      |    Weather           |    Pre-Calculated    |
|                      |                      |    Radio Range       |
+----------------------+----------------------+----------------------+
|                      |    Status            |    Omni DF Signal    |
|                      |                      |    Strength          |
+----------------------+----------------------+----------------------+
| **Responses**        |    Message           |    Area Object       |
|                      |    Digipeater Trace  |                      |
|                      |                      |    Wind Direction    |
|                      |                      |    and Speed         |
+----------------------+----------------------+----------------------+
|                      |    Stations Heard    |                      |
+----------------------+----------------------+----------------------+
|                      |    Heard Statistics  |                      |
+----------------------+----------------------+----------------------+
|                      |    Station           |                      |
|                      |    Capabilities      |                      |
+----------------------+----------------------+----------------------+
| **Status**           |    Time (DHM zulu)   |                      |
|                      |    Status text       |                      |
|                      |                      |                      |
|                      |    Meteor Scatter    |                      |
|                      |    Beam              |                      |
|                      |    Heading/Power     |                      |
|                      |    Maidenhead        |                      |
|                      |    Locator (Grid     |                      |
|                      |    Square) Altitude  |                      |
|                      |    (Mic-E)           |                      |
|                      |                      |                      |
|                      |    E-mail message    |                      |
+----------------------+----------------------+----------------------+
| **Other**            |    Third-Party       |                      |
|                      |    forwarding        |                      |
|                      |    Invalid Data/Test |                      |
|                      |    Data              |                      |
+----------------------+----------------------+----------------------+

..

   **Comment Field** In general, any APRS packet can contain a plain
   text comment (such as a beacon message) in the Information field,
   immediately following the APRS Data or APRS Data Extension.

   There is no separator between the APRS data and the comment unless
   otherwise stated.

   The comment may contain any printable ASCII characters (except **\|**
   and **~**, which are reserved for TNC channel switching).

   The maximum length of the comment field depends on the report —
   details are included in the description of each report.

   In special cases, the Comment field can also contain further APRS
   data:

-  **Altitude** in comment text (see Chapter 6: Time and Position
      Formats), or in Mic-E status text (see Chapter 10: Mic-E Data
      Format).

-  **Maidenhead Locator** (grid square), in a Mic-E status text field
      (see Chapter 10: Mic-E Data Format) or in a Status Report (see
      Chapter 16: Status Reports).

-  **Bearing and Number/Range/Quality** parameters (/BRG/NRQ), in DF
      reports (see Chapter 7: APRS Data Extensions).

-  **Area Object Line Widths** (see Chapter 11: Object and Item
      Reports).

-  **Signpost Objects** (see Chapter 11: Object and Item Reports).

-  **Weather and Storm Data** (see Chapter 12: Weather Reports).

-  **Beam Heading and Power**, in Status Reports (see Chapter 16: Status
      Reports).

..

   **Base-91 Notation** Two APRS data formats use base-91 notation:
   lat/long coordinates in compressed format (see Chapter 9) and the
   altitude in Mic-E format (see Chapter 10).

   Base-91 data is compressed into a short string of characters. All the
   characters are printable ASCII, with character codes in the range
   33–124 decimal (i.e. **!** through **\|**).

   To compute the base-91 ASCII character string for a given data value,
   the value is divided by progressively reducing powers of 91 until the
   remainder is less than 91. At each step, 33 is added to the modulus
   of the division process to obtain the corresponding ASCII character
   code.

   For example, for a data value of 12345678:

========================== ==== ===================================
   12345678 / 91\ :sup:`3`    =    modulus **16**, remainder 288542
========================== ==== ===================================
   288542 / 91\ :sup:`2`      =    modulus **34**, remainder 6988
   6988 / 91\ :sup:`1`        =    modulus **76**, remainder **72**
========================== ==== ===================================

..

   The four ASCII character codes are thus 49 (i.e. **16**\ +33), 67
   (i.e. **34**\ +33), 109 (i.e. **76**\ +33) and 105 (i.e.
   **72**\ +33), corresponding to the ASCII string **1Cmi**.

   **APRS Data Units** For historical reasons there is some lack of
   consistency between units of data in APRS packets — some speeds are
   in knots, others in miles per hour; some altitudes are in feet,
   others in meters, and so on. It is emphasized that this specification
   describes the units of data as they are transmitted on-air. It is the
   responsibility of APRS applications to convert the on-air units to
   more suitable units if required.

   The default GPS earth datum is World Geodetic System (WGS) 1984.

TIME AND POSITION FORMATS
=========================

   **Time Formats** APRS timestamps are expressed in three different
   ways:

-  Day/Hours/Minutes format

-  Hours/Minutes/Seconds format

-  Month/Day/Hours/Minutes format

..

   In all three formats, the 24-hour clock is used.

   **Day/Hours/Minutes** (DHM) format is a fixed 7-character field,
   consisting of a 6-digit *day/time* group followed by a single *time
   indicator* character (**z** or

   **/**). The day/time group consists of a two-digit day-of-the-month
   (01–31) and a four-digit time in hours and minutes.

   Times can be expressed in *zulu* (UTC/GMT) or *local* time. For
   example:

   092345\ **z** is 2345 hours *zulu* time on the 9th day of the month.

   092345\ **/** is 2345 hours *local* time on the 9th day of the month.

   It is recommended that future APRS implementations only transmit zulu
   format on the air.

   **Note**: The time in Status Reports may *only* be in zulu format.

   **Hours/Minutes/Seconds** (HMS) format is a fixed 7-character field,
   consisting of a 6-digit time in hours, minutes and seconds, followed
   by the **h** time-indicator character. For example:

   234517\ **h** is 23 hours 45 minutes and 17 seconds *zulu*.

   **Note:** This format may *not* be used in Status Reports.

   **Month/Day/Hours/Minutes** (MDHM) format is a fixed 8-character
   field, consisting of the month (01–12) and day-of-the-month (01–31),
   followed by the time in hours and minutes zulu. For example:

   10092345 is 23 hours 45 minutes zulu on October 9th.

   This format is only used in reports from stand-alone “positionless”
   weather stations (i.e. reports that do not contain station position
   information).

   **Use of Timestamps** When a station transmits a report *without* a
   timestamp, an APRS receiving station can make an internal record of
   the time it was received, if required. This record is the *receiving*
   station’s notion of the time the report was created.

   On the other hand, when a station transmits a report *with* a
   timestamp, that timestamp represents the *transmitting* station’s
   notion of the time the report was created.

   In other words, reports sent *without* a timestamp can be regarded as
   real-time, “current” reports (and the *receiving* station has to
   record the time they were received), whereas reports sent *with* a
   timestamp may or may not be real- time, and may possibly be (very)
   “old”.

   Four APRS Data Type Identifiers specify whether or not a report
   contains a timestamp, depending on whether the station has APRS
   messaging capability or not:

+------------------------+------------------+------------------------+
|                        |    **No APRS**   |    **With APRS         |
|                        |                  |    Messaging**         |
|                        |    **Messaging** |                        |
+========================+==================+========================+
| **(Current/real-time)  |    **!**         |    **=**               |
| Report without         |                  |                        |
| timestamp**            |                  |                        |
+------------------------+------------------+------------------------+
| **(Old/non-real-time)  |    **/**         |    **@**               |
| Report with            |                  |                        |
| timestamp**            |                  |                        |
+------------------------+------------------+------------------------+

..

   Stations without APRS messaging capability are typically stand-alone
   trackers or digipeaters. Stations reporting without a timestamp are
   generally (but not necessarily) fixed stations.

   **Latitude Format** Latitude is expressed as a fixed 8-character
   field, in degrees and decimal minutes (to two decimal places),
   followed by the letter **N** for north or **S** for south.

   Latitude degrees are in the range 00 to 90. Latitude minutes are
   expressed as whole minutes and hundredths of a minute, separated by a
   decimal point.

   For example:

   4903\ **.**\ 50\ **N** is 49 degrees 3 minutes 30 seconds north.

   In generic format examples, the latitude is shown as the 8-character
   string

   ddmm.hhN (i.e. degrees, minutes and hundredths of a minute north).

   **Longitude Format** Longitude is expressed as a fixed 9-character
   field, in degrees and decimal minutes (to two decimal places),
   followed by the letter **E** for east or **W** for west.

   Longitude degrees are in the range 000 to 180. Longitude minutes are
   expressed as whole minutes and hundredths of a minute, separated by a
   decimal point.

   For example:

   07201\ **.**\ 75\ **W** is 72 degrees 1 minute 45 seconds west.

   In generic format examples, the longitude is shown as the 9-character
   string

   dddmm.hhW (i.e. degrees, minutes and hundredths of a minute west).

   **Position Coordinates**

   Position coordinates are a combination of latitude and longitude,
   separated by a display Symbol Table Identifier, and followed by a
   Symbol Code. For example:

   4903\ **.**\ 50N\ **/**\ 07201.75W\ **-**

   The **/** character between latitude and longitude is the Symbol
   Table Identifier (in this case indicating use of the Primary Symbol
   Table), and the **–** character at the end is the Symbol Code from
   that table (in this case, indicating a “house” icon).

   A description of display symbols is included in Chapter 20: APRS
   Symbols. The full Symbol Table listing is in Appendix 2.

   **Position Ambiguity** In some instances — for example, where the
   exact position is not known — the sending station may wish to reduce
   the number of digits of precision in the latitude and longitude. In
   this case, the mm and hh digits in the latitude may be progressively
   replaced by a ␣ (space) character as the amount of imprecision
   increases. For example:

   4903.5␣N represents latitude to nearest 1/10th of a minute.

   4903.␣␣N represents latitude to nearest minute. 490␣.␣␣N represents
   latitude to nearest 10 minutes. 49␣␣.␣␣N represents latitude to
   nearest degree.

   The level of ambiguity specified in the latitude will automatically
   apply to the longitude as well — it is not necessary to include any ␣
   characters in the longitude.

   For example, the coordinates:

   4903\ **.**\ ␣␣N/07201.75W-

   represent the position to the nearest minute. That is, the hundredths
   of minutes of latitude and longitude may take any value in the range
   00–99.

   Thus the station may be located anywhere inside a bounding box having
   the following corner coordinates:

   North West corner: 49 deg 3.99 mins N, 72 deg 1.99 mins W

   North East corner: 49 deg 3.99 mins N, 72 deg 1.00 mins W

   South East corner: 49 deg 3.00 mins N, 72 deg 1.00 mins W

   South West corner: 49 deg 3.00 mins N, 72 deg 1.99 mins W

   **Default Null Position**

   Where a station does not have *any* specific position information to
   transmit (for example, a Mic-E unit without a GPS receiver connected
   to it), the station must transmit a default null position in the
   location field.

   The null position corresponds to 0° 0' 0" north, 0° 0' 0" west.

   The null position should be include the **\\.** symbol
   (unknown/indeterminate position). For example, a Position Report for
   a station with unknown position will contain the coordinates
   …0000.00N\ **\\**\ 00000.00W\ **.…**

**Maidenhead**

   **Locator (Grid Square)**

   An alternative method of expressing a station’s location is to
   provide a Maidenhead locator (grid square). There are four ways of
   doing this:

-  In a Status Report — e.g. IO91SX/-

..

   (/- represents the symbol for a “house”).

-  In Mic-E Status Text — e.g. IO91SX\ **/G**

..

   (**/G** indicates a “grid square”).

-  In the Destination Address — e.g. IO91SX. (obsolete).

-  In AX.25 beacon text, with the **[** APRS Data Type Identifier — e.g.

..

   **[**\ IO91SX] (obsolete).

   Grid squares may be in 6-character form (as above) or in the
   shortened 4-character form (e.g. IO91).

   **NMEA Data** APRS recognizes raw ASCII data strings conforming to
   the NMEA 0183 Version 2.0 specification, originating from navigation
   equipment such as GPS and LORAN receivers. It is recommended that
   APRS stations interpret at least the following NMEA Received Sentence
   types:

   GGA Global Positioning System Fix Data

   GLL Geographic Position, Latitude/Longitude Data

   RMC Recommended Minimum Specific GPS/Transit Data VTG Velocity and
   Track Data

   WPT Way Point Location

   **Altitude** Altitude may be expressed in two ways:

-  In the comment text.

-  In Mic-E format.

..

   **Altitude in Comment Text** — The comment may contain an altitude
   value, in the form **/A=**\ aaaaaa, where aaaaaa is the altitude in
   feet. For example:

   /A=001234. The altitude may appear anywhere in the comment.

   **Altitude in Mic-E format** — The optional Mic-E status field can
   contain altitude data. See Chapter 10: Mic-E Data Format.

APRS DATA EXTENSIONS
====================

   A fixed-length 7-byte field may follow APRS position data. This field
   is an APRS Data Extension. The extension may be one of the following:

-  CSE\ **/**\ SPD Course and Speed (this may be followed by a further 8
      bytes containing DF bearing and Number/Range/Quality parameters)

-  DIR\ **/**\ SPD Wind Direction and Wind Speed

-  **PHG**\ phgd Station Power and Effective Antenna Height/Gain/
      Directivity

-  **RNG**\ rrrr Pre-Calculated Radio Range

-  **DFS**\ shgd DF Signal Strength and Effective Antenna Height/Gain

-  Tyy/Cxx Area Object Descriptor

..

   **Course and Speed** The 7-byte CSE\ **/**\ SPD Data Extension can be
   used to represent the course and speed of a vehicle or APRS Object.

   The course is expressed in degrees (001-360), clockwise from due
   north. The speed is expressed in knots. A slash **/** character
   separates the two.

   For example:

   088/036 represents a course 88 degrees, traveling at 36 knots.

   If the course and speed are unknown or not relevant, they can be set
   to

   **000/000** or **.../...** or **␣␣␣/␣␣␣**.

   **Note**: In the special case of DF reports, a course of 000 means
   that the DF station is fixed. If the course is non-zero, the station
   is mobile.

   **Wind Direction and Wind Speed**

   The 7-byte DIR\ **/**\ SPD Data Extension can be used to represent
   the wind direction and sustained one-minute wind speed in a Weather
   Report.

   The wind direction is expressed in degrees (001-360), clockwise from
   due north. The speed is expressed in knots. A slash **/** character
   separates the two.

   For example:

   220/004 represents a wind direction of 220 degrees and a speed of 4
   knots.

   If the wind direction and speed are unknown or not relevant, they can
   be set to **000/000** or **.../...** or **␣␣␣/␣␣␣**.

   **Power, Effective Antenna**

   **Height/Gain/ Directivity**

PHG Codes
---------

   The 7-byte **PHG**\ phgd Data Extension specifies the transmitter
   power, effective antenna height-above-average-terrain, antenna gain
   and antenna directivity. APRS uses this information to plot radio
   range circles around stations.

   The 7 characters of this Data Extension are encoded as follows:
   Characters 1–3: **PHG** (fixed)

   Character 4: p Power code Character 5: h Height code Character 6: g
   Antenna gain code Character 7: d Directivity code

   The PHG codes are listed in the table below:

+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
| phgd  |       |       |       |       |       |       |       |       |       |       |       |
| **Co  | **0** | **1** | **2** | **3** | **4** | **5** | **6** | **7** | **8** | **9** |  **Un |
| de:** |       |       |       |       |       |       |       |       |       |       | its** |
+=======+=======+=======+=======+=======+=======+=======+=======+=======+=======+=======+=======+
| Power |    0  |    1  |    4  |    9  |    16 |    25 |    36 |    49 |    64 |    81 |       |
|       |       |       |       |       |       |       |       |       |       |       | watts |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
| H     |    10 |    20 |    40 |    80 |       |       |       |       |       |       |       |
| eight |       |       |       |       |   160 |   320 |   640 |  1280 |  2560 |  5120 |  feet |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
| Gain  |    0  |    1  |    2  |    3  |    4  |    5  |    6  |    7  |    8  |    9  |    dB |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
| D     |       |    45 |    90 |       |       |       |       |       |       |       |       |
| irect |  omni |       |       |   135 |   180 |   225 |   270 |   315 |   360 |       |   deg |
| ivity |       |    NE |    E  |       |       |       |       |       |       |       |       |
|       |       |       |       |    SE |    S  |    SW |    W  |    NW |    N  |       |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+

..

   The height code represents the effective height of the antenna *above
   average local terrain*, not above ground or sea level — this is to
   provide a rough indication of the antenna’s effectiveness in the
   local area .

   The height code may in fact be any ASCII character 0–9 and above.
   This is so that larger heights for balloons, aircraft or satellites
   may be specified.

   For example:

   **:** is the height code for 10240 feet (approximately 1.9 miles).

   **;** is the height code for 20480 feet (approximately 3.9 miles),
   and so on.

   The Directivity code offsets the PHG circle by one third in the
   indicated direction. This means a front-to-back ratio of 2 to 1. Most
   often this is used to indicate a favored direction or a null, even if
   an omni antenna is at the site.

   An example of the PHG Data Extension:

   PHG5132 means a power of 25 watts,

   an antenna height of 20 feet above the average local terrain, an
   antenna gain of 3 dB,

   and maximum gain due east.

   **Range Circle Plot** On receipt, APRS uses the **p**, **h**, **g**
   and **d** codes to calculate the usable radio range (in miles), for
   plotting a range circle representing the local radio horizon around
   the station. The radio range is calculated as follows:

   power = **p**\ 2

   Height-above-average-terrain (haat) = 10 x 2\ **h**

   gain = 10(**g**/10)

   range = –( 2 x haat x –( (power/10) x (gain/2) ) ) Thus, for PHG5132:

   power = **5**\ 2 = 25 watts

   haat = 10 x 2\ **1** = 20 feet

   gain = 10(**3**/10) = 1.995262

   range = –( 2 x 20 x –( (25/10) x (1.995262/2) ) )

   ~ 7.9 miles

   As the direction of maximum gain is due east, APRS will draw a range
   circle of radius 8 miles around the station, offset by 2.7 miles
   (i.e. one third of 8 miles) in an easterly direction.

   **Note**: In the absence of any PHG data, stations are assumed to be
   running 10 watts to a 3dB omni antenna at 20 feet, resulting in a
   6-mile radius range circle, centered on the station.

   **Pre-Calculated Radio Range**

   The 7-byte **RNG**\ rrrr Data Extension allows users to transmit a
   pre- calculated omni-directional radio range, where rrrr is the range
   in miles (with leading zeros).

   For example, RNG0050 indicates a radio range of 50 miles. APRS can
   use this value to plot a range circle around the station.

   **Omni-DF Signal**

   **Strength**

   The 7-byte **DFS**\ shgd Data Extension lets APRS localize jammers by
   plotting the overlapping signal strength contours of all stations
   hearing the signal.

   This Omni-DF format replaces the PHG format to indicate DF signal
   strength, in that the transmitter power field is replaced with the
   relative signal strength (s) from 0 to 9.

DFS Codes
---------

+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
| shgd  |       |       |       |       |       |       |       |       |       |       |       |
| **Co  | **0** | **1** | **2** | **3** | **4** | **5** | **6** | **7** | **8** | **9** |  **Un |
| de:** |       |       |       |       |       |       |       |       |       |       | its** |
+=======+=======+=======+=======+=======+=======+=======+=======+=======+=======+=======+=======+
| Str   |    0  |    1  |    2  |    3  |    4  |    5  |    6  |    7  |    8  |    9  |       |
| ength |       |       |       |       |       |       |       |       |       |       |   S-p |
|       |       |       |       |       |       |       |       |       |       |       | oints |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
| H     |    10 |    20 |    40 |    80 |       |       |       |       |       |       |       |
| eight |       |       |       |       |   160 |   320 |   640 |  1280 |  2560 |  5120 |  feet |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
| Gain  |    0  |    1  |    2  |    3  |    4  |    5  |    6  |    7  |    8  |    9  |    dB |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
| D     |       |    45 |    90 |       |       |       |       |       |       |       |       |
| irect |  omni |       |       |   135 |   180 |   225 |   270 |   315 |   360 |       |   deg |
| ivity |       |    NE |    E  |       |       |       |       |       |       |       |       |
|       |       |       |       |    SE |    S  |    SW |    W  |    NW |    N  |       |       |
+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+

..

   For example, DFS2360 represents a weak signal (around strength S2)
   heard on an omni antenna with 6 dB gain at 80 feet.

   A signal strength of zero (0) is particularly significant, because
   APRS uses these 0 signal reports to draw (usually black) circles
   where the jammer is *not* heard. These black circles are extremely
   valuable since there will be a lot more reports from stations that do
   not hear the jammer than from those that do. This quickly eliminates
   a lot of territory.

   **Bearing and Number/Range/**

**Quality**

   DF reports contain an 8-byte field **/**\ BRG\ **/**\ NRQ that
   follows the CSE\ **/**\ SPD Data Extension, specifying the course,
   speed, bearing and NRQ (Number/Range/ Quality) value of the report.
   NRQ indicates the Number of hits, the approximate Range and the
   Quality of the report.

   For example, in:

   …088/036/270/729… course = 88 degrees, speed = 36 knots,

   bearing = 270 degrees, N = 7, R = 2, Q = 9

   If N is 0, then the NRQ value is meaningless. Values of N from 1 to 8
   give an indication of the number of hits per period relative to the
   length of the time period — thus a value of 8 means 100% of all
   samples possible got a hit. A value of 9 for N indicates to other
   users that the report is manual.

   The N value is not processed, but is just another indicator from the
   automatic DF units.

   The range limits the length of the line to the original map’s scale
   of the sending station. The range is 2R so, for R=4, the range will
   be 16 miles.

   Q is a single digit in the range 0–9, and provides an indication of
   bearing accuracy:

   If the course and speed parameters are not appropriate, they should
   have the value **000/000** or **.../...** or **␣␣␣/␣␣␣**.

   **Area Object Descriptor**

   The 7-byte Tyy/Cxx Data Extension is an Area Object Descriptor. The T

   parameter specifies the type of object (square, circle, triangle,
   etc) and the

   /C parameter specifies its fill color.

   Area Objects are described in Chapter 11: Object and Item Reports.

POSITION AND DF REPORT DATA FORMATS
===================================

   **Position Reports** Lat/Long Position Reports are contained in the
   Information field of an APRS AX.25 frame.

   The following diagrams show the permissible formats of these reports,
   together with some examples. The gray areas indicate optional fields,
   and the shaded (yellow) characters are literal ASCII characters. In
   all cases there is a maximum of 43 characters after the Symbol Code.

   Bytes:

   Bytes:

   Bytes:

   Bytes:

   Bytes:

   Bytes:

   Bytes:

   **DF Reports** DF Reports are contained in the Information field of
   an APRS AX.25 frame. The Bearing and Number/Range/Quality (BRG/NRQ)
   parameters follow the Data Extension field.

   **Note**: The BRG/NRQ parameters are only meaningful when the report
   contains the DF symbol (i.e. the Symbol Table ID is **/** and the
   Symbol Code is **\\**).

   **Note**: If the DF station is fixed, the Course value is zero. If
   the station is moving, the Course value is non-zero.

   Bytes:

COMPRESSED POSITION REPORT DATA FORMATS
=======================================

   In compressed data format, the Information field contains the
   station’s latitude and longitude, together with course and speed or
   pre-calculated radio range or altitude.

   This information is compressed to minimize the length of the
   transmitted packet (and therefore improve its chances of being
   received correctly under less than ideal conditions).

   The Information field also contains a display Symbol Code, and there
   may optionally be a plain text comment (uncompressed) as well.

   **The Advantages of Data Compression**

   Compressed data format may be used in place of the numeric lat/long
   coordinates already described, such as in the **!**, **/**, **@** and
   **=** formats.

   Data compression has several important benefits:

-  Fully backwards compatible with all existing formats.

-  Fully supports any comment string.

-  Speed is accurate to +/-1 mph up to about 40 mph and within 3% at 600
      mph.

-  Altitude in feet is accurate to +/- 0.4% from 1 foot to 3000 miles.

-  Consistent one-algorithm processing of compressed latitude and
      longitude.

-  Improved position to 1 foot worldwide.

-  Pre-calculated radio range, compressed to one byte.

-  Potential 50% compression of every position format on the air.

-  Potential 40% reduction of raw GPS NMEA data length.

-  Additional 7-byte reduction for NEMA GGA altitudes.

-  Support for TNC compression at the NMEA source (from the GPS
      receiver).

-  Digipeater compression of old NMEA trackers on the fly.

-  Usage is optional in all cases.

..

   The only minor disadvantages are that the course only resolves to +/-
   2 degrees, and this format does not support PHG.

**Compressed Data**

**Format**

Bytes:

   Compressed data may be generated in several ways:

-  by APRS software.

-  pre-entered manually into a digipeater’s beacon text.

-  by a digipeater converting raw tracker NMEA packets to compressed.

..

   [In future, there is the possibility that a Kantronics KPC-3 or other
   tracker TNC will be able to compress data directly from an attached
   GPS receiver].

   In all cases the compressed format is a fixed 13-character field:

   /YYYYXXXX$csT

   where / is the Symbol Table Identifier YYYY is the compressed
   latitude XXXX is the compressed longitude

   $ is the Symbol Code

   cs is the compressed course/speed or compressed pre-calculated radio
   range or compressed altitude

   T is the compression type indicator

+----------+----------+----------+----------+----------+----------+
|    **Co  |          |          |          |          |          |
| mpressed |          |          |          |          |          |
|          |          |          |          |          |          |
| Position |          |          |          |          |          |
|          |          |          |          |          |          |
|   Data** |          |          |          |          |          |
+==========+==========+==========+==========+==========+==========+
|    **Sym |    **Co  |    **Co  |          |    **Co  |          |
|    Table | mpressed | mpressed | **Symbol | mpressed |   **Comp |
|    ID**  |    Lat** |          |          |          |          |
|          |    YYYY  |   Long** |   Code** |   Course |   Type** |
|          |          |    XXXX  |          | /Speed** |    T     |
+----------+----------+----------+----------+----------+----------+
|          |          |          |          |    **Co  |          |
|          |          |          |          | mpressed |          |
|          |          |          |          |    Radio |          |
|          |          |          |          |          |          |
|          |          |          |          |  Range** |          |
+----------+----------+----------+----------+----------+----------+
|          |          |          |          |    **Co  |          |
|          |          |          |          | mpressed |          |
|          |          |          |          |    Al    |          |
|          |          |          |          | titude** |          |
+----------+----------+----------+----------+----------+----------+
|    1     |    4     |    4     |    1     |    2     |    1     |
+----------+----------+----------+----------+----------+----------+

..

   Compressed format can be used in place of lat/long position format
   anywhere that …ddmm.hhN/dddmm.hhW$xxxxxxx… occurs.

   All bytes except for the **/** and **$** are base-91 printable ASCII
   characters (**!**..\ **{**). These are converted to numeric values by
   subtracting 33 from the decimal ASCII character code. For example,
   **#** has an ASCII code of 35, and represents a numeric value of 2
   (i.e. 35-33).

   **Symbol** The presence of the leading Symbol Table Identifier
   instead of a digit indicates that this is a compressed Position
   Report and not a normal lat/long report.

   **Lat/Long Encoding** The values of YYYY and XXXX are computed as
   follows:

   YYYY is 380926 x (90 – latitude) [base 91]

   latitude is positive for north, negative for south, in degrees.

   XXXX is 190463 x (180 + longitude) [base 91]

   longitude is positive for east, negative for west, in degrees.

   For example, for a longitude of 72° 45' 00" west (i.e. -72.75
   degrees), the math is 190463 x (180 – 72.75) = 20427156. Because this
   is to base 91, it is then necessary to progressively divide this
   value by reducing powers of 91, to obtain the numerical values of X:

   20427156 / 91\ :sup:`3` = **27**, remainder 80739

   80739 / 91\ :sup:`2` = **9**, remainder 6210

   6210 / 91\ :sup:`1` = **68**, remainder **22**

   To obtain the corresponding ASCII characters, 33 is added to each of
   these values, yielding 60 (i.e. 27+33), 42, 101 and 55. From the
   ASCII Code Table (in Appendix 3), this corresponds to **<*e7** for
   XXXX.

   **Lat/Long Decoding** To decode a compressed lat/long, the reverse
   process is needed. That is, if

   YYYY is represented as
   y\ :sub:`1`\ y\ :sub:`2`\ y\ :sub:`3`\ y\ :sub:`4` and XXXX as
   x\ :sub:`1`\ x\ :sub:`2`\ x\ :sub:`3`\ x\ :sub:`4`, then:

   Lat = 90 - ((y\ :sub:`1`-33) x 91\ :sup:`3` + (y\ :sub:`2`-33) x
   91\ :sup:`2` + (y\ :sub:`3`-33) x 91 + y\ :sub:`4`-33) / 380926

   Long = -180 + ((x\ :sub:`1`-33) x 91\ :sup:`3` + (x\ :sub:`2`-33) x
   91\ :sup:`2` + (x\ :sub:`3`-33) x 91 + x\ :sub:`4`-33) / 190463

   For example, if the compressed value of the longitude is **<*e7** (as
   computed above), the calculation becomes:

Long = -180 + (27 x 91\ :sup:`3` + 9 x 91\ :sup:`2` + 68 x 91 + 22) /
190463

= -180 + (20346417 + 74529 + 6188 + 22) / 190463

   = -180 + 107.25

   = -72.75 degrees

   **Course/Speed, Pre-Calculated Radio Range and**

**Altitude**

   The two cs bytes following the Symbol Code character can contain
   either the compressed course and speed or the compressed
   pre-calculated radio range or the station’s altitude. These two bytes
   are in base 91 format.

   In the special case of c = **␣** (space), there is no course, speed
   or range data, in which case the csT bytes are ignored.

   **Course/Speed** — If the ASCII code for c is in the range **!** to
   **z** inclusive — corresponding to numeric values in the range 0–89
   decimal (i.e. after subtracting 33 from the ASCII code) — then cs
   represents a compressed course/speed value:

   course = **c** x 4

   speed = 1.08\ **s** – 1

   For example, if the cs characters are **7P**, the corresponding
   values of **c** and **s** (after subtracting 33 from the ASCII
   character code) are 22 and 47 respectively. Substituting these values
   in the above equations:

   course = **22** x 4 = 88 degrees

   speed = 1.08\ **47** – 1 = 36.2 knots

   **Pre-Calculated Radio Range** — If c = **{**, then cs represents a
   compressed pre-calculated radio range value:

   range = 2 x 1.08\ **s**

   For example, if the cs bytes are **{?**, the ASCII code for **?** is
   63, so the value of **s** is 30 (i.e. 63-33). Thus:

   range = 2 x 1.08\ **30**

   ~ 20 miles

   So APRS will draw a circle of radius 20 miles around the station plot
   on the screen.

   **The Compression Type (T) Byte**

Bit:

Value:

   The T byte follows the cs bytes. The T byte contains several bit
   fields showing the GPS fix status, the NMEA source of the position
   data and the origin of the compression.

   The T byte is not meaningful if the c byte is **␣** (space).

+--------+--------+--------+--------+--------+------+---+---+
|    *   |        |        |        |        |      |   |   |
| *Compr |        |        |        |        |      |   |   |
| ession |        |        |        |        |      |   |   |
|        |        |        |        |        |      |   |   |
|   Type |        |        |        |        |      |   |   |
|    (T) |        |        |        |        |      |   |   |
|        |        |        |        |        |      |   |   |
|   Byte |        |        |        |        |      |   |   |
|    Fo  |        |        |        |        |      |   |   |
| rmat** |        |        |        |        |      |   |   |
+========+========+========+========+========+======+===+===+
|    7   |    6   |    5   |    4   |    3   |    2 | 1 | 0 |
+--------+--------+--------+--------+--------+------+---+---+
|        |        |        |        |    *   |      |   |   |
|   *Not |   *Not |  **GPS | **NMEA | *Compr |      |   |   |
|        |        |        |    So  | ession |      |   |   |
|  used* |  used* |  Fix** | urce** |    Or  |      |   |   |
|        |        |        |        | igin** |      |   |   |
+--------+--------+--------+--------+--------+------+---+---+
|    0   |    0   |    0 = |    0 0 |    0 0 |      |   |   |
|        |        |    old |    =   |    0 = |      |   |   |
|        |        |        |        |        |      |   |   |
|        |        | (last) |  other |   Comp |      |   |   |
|        |        |        |        | ressed |      |   |   |
+--------+--------+--------+--------+--------+------+---+---+
|        |        |    1 = |    0 1 |    0 0 |      |   |   |
|        |        |    c   |    =   |    1 = |      |   |   |
|        |        | urrent |    GLL |    TNC |      |   |   |
|        |        |        |        |        |      |   |   |
|        |        |        |        |  BText |      |   |   |
+--------+--------+--------+--------+--------+------+---+---+
|        |        |        |    1 0 |    0 1 |      |   |   |
|        |        |        |    =   |    0 = |      |   |   |
|        |        |        |    GGA |    So  |      |   |   |
|        |        |        |        | ftware |      |   |   |
|        |        |        |        |        |      |   |   |
|        |        |        |        |  (DOS/ |      |   |   |
|        |        |        |        | Mac/Wi |      |   |   |
|        |        |        |        | n/+SA) |      |   |   |
+--------+--------+--------+--------+--------+------+---+---+
|        |        |        |    1 1 |    0 1 |      |   |   |
|        |        |        |    =   |    1 = |      |   |   |
|        |        |        |    RMC |        |      |   |   |
|        |        |        |        |  [tbd] |      |   |   |
+--------+--------+--------+--------+--------+------+---+---+
|        |        |        |        |    1 0 |      |   |   |
|        |        |        |        |    0 = |      |   |   |
|        |        |        |        |        |      |   |   |
|        |        |        |        |   KPC3 |      |   |   |
+--------+--------+--------+--------+--------+------+---+---+
|        |        |        |        |    1 0 |      |   |   |
|        |        |        |        |    1 = |      |   |   |
|        |        |        |        |        |      |   |   |
|        |        |        |        |   Pico |      |   |   |
+--------+--------+--------+--------+--------+------+---+---+
|        |        |        |        |    1 1 |      |   |   |
|        |        |        |        |    0 = |      |   |   |
|        |        |        |        |        |      |   |   |
|        |        |        |        |  Other |      |   |   |
|        |        |        |        |    t   |      |   |   |
|        |        |        |        | racker |      |   |   |
|        |        |        |        |        |      |   |   |
|        |        |        |        |  [tbd] |      |   |   |
+--------+--------+--------+--------+--------+------+---+---+
|        |        |        |        |    1 1 |      |   |   |
|        |        |        |        |    1 = |      |   |   |
|        |        |        |        |        |      |   |   |
|        |        |        |        |   Digi |      |   |   |
|        |        |        |        | peater |      |   |   |
|        |        |        |        |        |      |   |   |
|        |        |        |        |   conv |      |   |   |
|        |        |        |        | ersion |      |   |   |
+--------+--------+--------+--------+--------+------+---+---+

..

   For example, if the compressed position was derived from an RMC
   sentence, the fix is current, and the compression was performed by
   APRSdos software, then the value of T in binary is 0 0 1 11 010,
   which equates to 58 decimal.

   Adding 33 to this value gives the ASCII code for the T byte (i.e.
   91), which

   corresponds to the **[** character.

   Thus, using data from all the earlier examples, if the RMC sentence
   contains (among other parameters) the following data:

   Latitude = 49° 30' 00" north

   Longitude = 72° 45' 00" west Speed = 36.2 knots

   Course = 88°

   and: the fix is current

   compression is performed by APRSdos software the display symbol is a
   “car”

   then the complete 13-character compressed location field is
   transmitted as:

===== ======== ======== ======== ==========
/     YYYY     XXXX        $        csT
===== ======== ======== ======== ==========
**/** **5L!!** **<*e7**    **>**    **7P[**
===== ======== ======== ======== ==========

..

   **Altitude** If the T byte indicates that the raw data originates
   from a GGA sentence (i.e. bits 4 and 3 of the T byte are 10), then
   the sentence contains an altitude value, in feet. After compression,
   the compressed altitude data is placed in the cs bytes, such that:

   altitude = 1.002\ **cs** feet

   For example, if the received cs bytes are **S]**, the computation is
   as follows:

-  Subtract 33 from the ASCII code for each character:

..

   **c** = 83 – 33 = 50

   **s** = 93 – 33 = 60

-  Multiply **c** by 91 and add **s** to obtain **cs**: **cs** = 50 x 91
      + 60

..

   = 4610

-  Then altitude = 1.002\ **4610**

= 10004 feet

   **New Trackers** Tracker firmware may compress GPS data directly to
   APRS compressed format. They would use the **!** Data Type Indicator,
   showing that the position is real-time and that the tracker is not
   APRS-capable.

   If the Position Report is not real-time, then the **/** Data Type
   Indicator can be used instead, so that the latest fix time may be
   included.

.. |image0| image:: media/image1.png
