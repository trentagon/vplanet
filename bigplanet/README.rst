BigPlanet
-----
A suite of data analysis and extraction routines for ``VPLanet``.

Overview
========


Installation
============
Navigate to the BigPlanet directory (this directory) and run the ``setup`` script
by entering ``python setup.py install``, which installs various dependencies and allows
BigPlanet to be run from the command line (see running bigplanet section below)

Running BigPlanet
=================
BigPlanet has two primary uses: the command line to generate the HDF5 file, and
the module that is imported into python scripts for data extraction. These are explained in
detail below.

Command Line Usage
==================
Using BigPlanet on the command line is relatively straight forward. After a simulation
has completed, simply run the following command in the in the command line:

.. code-block:: bash

    bigplanet <input file> --c [number of cores]

where the input file is the same file used to run vspace and multi-planet. There
is an optional argument which is the number of processors used. The default number
of processors is the maximum number on the machine.

Module Usage
============
Using BigPlanet as a module is where majority of the *magic* happens. To start,
import BigPlanet as a module:

.. code-block:: python

    import bigplanet as bp

This allows us to use the various functions that are outlined in detail below, such as
print all the names of the variables in the HDF5 file (PrintKeys), extract a particular
variable known as a key (ExtractColumn), Extract the units of a particular key value
(ExtractUnits),extract unique values in a particular key (ExtractUniqueValues),
create a Matrix based on two keys (CreateMatrix) and writing out a list of keys
to a csv file (WriteOutput).

.. note::

	  Keys using the following format for naming: body_variable_aggregation


**PrintKeys**

PrintKeys is a simple function that prints out all available keys. Keys, as mentioned above,
are the names of various variables that can be extracted. It takes in the following arguments:

.. code-block:: python

    PrintKeys(HDF5_File)

where *HDF5_File* is the name of the HDF5 file, which is used like so:

.. code-block:: python

    HDF5_File = h5py.File(filename, 'r')



**ExtractColumn**

ExtractColumn is a function that returns all of values of a particular column in the
HDF5 file. It takes the following arguments:

.. code-block:: python

    ExtractColumn(HDF5_File,Key)

where:

*HDF5_File* is the name of the HDF5 file

*Key* is the name of the particular variable you are extracting the units from.

See the `Understanding Keys`_ Section for an indepth look at the types of key options available.



**ExtractUnits**

ExtractUnits is a function that returns the units of a particular column in the
HDF5 file. It takes the following arguments:

.. code-block:: python

    ExtractUnits(HDF5_File,Key)

where:

*HDF5_File* is the name of the HDF5 file

*Key* is the name of the particular variable you are extracting the units from.

See the `Understanding Keys`_ Section for an indepth look at the types of key options available.



**ExtractUniqueValues**

ExtractUniqueValues is a function that returns a list of unique values in a key provided.
It takes the following arguments:

.. code-block:: python

    ExtractUniqueValues(HDF5_File,Key)

where:

*HDF5_File* is the name of the HDF5 file

*Key* is the name of the particular variable you are extracting the units from.



**CreateMatrix**

CreateMatrix is a function that returns the zaxis for a 3D matrix. This is useful
for plotting Contour Plots of the data extracted. CreateMatrix takes the following
arguments:

.. code-block:: python

    CreateMatrix(xaxis,yaxis,zarray)

where:

*xaxis* is the ExtractUniqueValues() of the column you want the xaxis to be

*yaxis* is the ExtractUniqueValues() of the column you want the xaxis to be

*zarray* is the ExtractColumn() of what you want the zaxis to be



**WriteOutput**

WriteOutput is a function that writes the list of columns to an output file. Headers
are optional. WriteOutput takes the following arguments:

.. code-block:: python

    WriteOutput(inputfile, columns, file="bigplanet.out", delim=" ", header=False, ulysses=False)

where:

*inputfile* is the name of the HDF5 file

*columns* is the list of keys you are extracting (Use the same format as ExtractColumn, ExtractUnits and
ExtractUniqueValues)

*File* is the name of the output file

*delim* is the delimiter for the output file (the default is spaces)

*header* adds the names and units for each column (default is False)

*ulysses* makes the file compatable with VR Ulysses (default is False)



Understanding Keys
==================
Keys are the bread and butter of BigPlanet. The keys, as briefly mentioned above,
are the names of the various variables that BigPlanet has extracted from the forward file
and the log file that are generated when VPLanet finishes compiling.

.. note::

	  Keys using the following format for naming: body_variable_aggregation

Below is a table of all the various aggregations available at this time:

.. list-table::
   :widths: auto
   :header-rows: 1

   * - Aggregation
     - Description
     - Usage
   * - Initial
     - returns a list of the *initial* values of the particular parameter for
       every simulation
     - body_variable_initial
   * - Final
     - returns a list of the *final* values of the particular parameter for
       every simulation
     - body_variable_final
   * - Output Order
     - returns a list of the names and units of the forward file values
     - body_variable_forward
   * - Forward
     - returns a nested list of the *forward* values of the particular
       parameter for every simulation
     - body_variable_forward


.. warning::

  The following aggregations will **only** work with parameters that are from the *forward* file.
  If you attempt to use it with a value that is **NOT** in the forward file, it will produce an error



 .. list-table::
    :widths: auto
    :header-rows: 1

    * - Aggregation
      - Description
      - Usage
    * - Min
      - returns a list of the minimum values from the *forward* values of the
        particular parameter for every simulation
      - body_variable_min
    * - Max
      - returns a list of the maximum values from the *forward* values of the
        particular parameter for every simulation
      - body_variable_max
    * - Mean
      - returns a list of the mean calculated from the *forward* values of the
        particular parameter for every simulation
      - body_variable_mean
    * - Geometric Mean
      - returns a list of the gemoetric mean calculated from the *forward*
        values of the particular parameter for every simulation
      - body_variable_geomean
    * - Standard Deviation
      - returns a list of the standard deviation calculated from the *forward*
        values of the particular parameter for every simulation
      - body_variable_stddev

Examples Using BigPlanet
========================
Below are links to various repositories showcasing the various uses of BigPlanet:
