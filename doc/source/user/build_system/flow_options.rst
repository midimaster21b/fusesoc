.. _ug_build_system_flow_options:

Configuring a flow
==================

FuseSoC uses `Edalize <https://github.com/olofk/edalize>`_ to chain together and run EDA tools. FuseSoC abstracts away many differences between :term:`tools <tool>` and tries to provide sane defaults to build many designs out of the box with no further configuration required. However, not all tool-specific details can be hidden.
At the same time, a certain level of tool-specific configurability is required to make full use of the features available in different tools.
Flow options are FuseSoC's way of customizing the way tools are used to build the design and how they are connected.

There are two categories of options available for the Edalize backends. Options that affect how the tools are chained together (the flow graph) and options for the individual tools to be run as part of the flow. This means that some tool options only become available if the corresponding tool becomes available due to a flow option being set to a certain value.



The example below shows how tool options for Icarus Verilog (``icarus``) and Mentor ModelSim (``modelsim``) are set.

* The ``iverilog`` binary will be called with the ``-g2012`` command-line argument, indicating that SystemVerilog 2012 support should be enabled.
* Similarily, for ModelSim the argument ``-timescale=1ns/1ns`` will be passed to the ``vlog`` binary, which elaborates the design.

.. code-block:: yaml

   # A fragment from blinky.core
   # ...
   targets:
     sim:
       # ...
       tools:
         icarus:
           iverilog_options:
             - -g2012 # Use SystemVerilog-2012
         modelsim:
           vlog_options:
             - -timescale=1ns/1ns

.. note::

   Where to find tool-specific code in FuseSoC

   The tool-specific code is provided by the `edalize library <https://github.com/olofk/edalize>`_.
   Most files, such as project files and Makefiles, are templates within edalize and can be improved easily if necessary.
   Please open an issue at the `edalize issue tracker on GitHub <https://github.com/olofk/edalize/issues>`_ to suggest improvements to tool-specific code.
