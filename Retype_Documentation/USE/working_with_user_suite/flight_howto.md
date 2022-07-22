---
order: 90
label: Flight HowTo
icon: 
---

.. _flight-howto:

Flight HowTo
============

The Flight User Suite comes with built-in guides to assist with usage of the research environment from setting up the flight environment to using the queue system.

Showing Available Guides
------------------------

To show the available guides, list them with::

    [flight@gateway1 (scooby) ~]$ flight howto ls
    â”Œâ”€â”€â”€â”€â”€â”€â”€â”¬â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”
    â”‚ Index â”‚ Name                             â”‚
    â”œâ”€â”€â”€â”€â”€â”€â”€â”¼â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”¤
    â”‚ 1     â”‚ Get Started                      â”‚
    â”‚ 2     â”‚ Work With The Flight Environment â”‚
    â”‚ 3     â”‚ Use Flight User Suite            â”‚
    â”‚ 4     â”‚ Run Jobs                         â”‚
    â”‚ 5     â”‚ Use A Scheduler                  â”‚
    <snip>

Viewing a Guide
---------------

A guide can be viewed by requesting either the index or name of the desired guide. When viewing a guide, the content will open inside a ``less`` session. 

To view the get started guide by name::

    [flight@gateway1 (scooby) ~]$ flight howto show 'Get Started'

To view the get started guide by index::

    [flight@gateway1 (scooby) ~]$ flight howto show 1

When finished with the guide, simply escape the ``less`` session with ``q``. Alternatively, the optional argument ``--no-pager`` will prevent any sort of view manager, instead the contents of the guide will be output straight to the terminal.

