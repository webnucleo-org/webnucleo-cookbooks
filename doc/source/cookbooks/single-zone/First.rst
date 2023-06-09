.. _first_calculation:

First Calculation
=================

Once you have :doc:`installed <../installation/code_installation>`
the network code,
run a first calculation.  First, retrieve the network data.
In the directory in which the code resides, type::

     $ make data

Next, type::

     $ ./single_zone_network --example

That will output an example usage. Copy that command into your command line
and hit enter.  The code will take a few minutes to run.
The output is left in a file *out.xml*.
You can analyze the calculation from this file.
For example, open Python by typing::

     $ python

and then, in Python, enter the commands::

     >>> import wnutils.xml as wx
     >>> xml = wx.Xml('out.xml')
     >>> xml.plot_property_vs_property('time', 't9', xlim = [0,1], xlabel = 'time (s)', ylabel = '$T_9$')

That `shows <https://osf.io/xhjrt>`_
the temperature (in billions of K) as a function of time.  Next,
enter::

     >>> xml.plot_mass_fractions_vs_property('time', ['n', 'h1', 'he4', 'si28', 'ni56'], xscale = 'log', yscale = 'log', ylim = [1.e-10,1], xlabel = 'time (s)', ylabel = 'Mass Fractions', use_latex_names = True, xlim = [1.e-15, 100])

Here you will `see <https://osf.io//f6w29>`_
the mass fractions of various species as a function of
time in the calculation.

You can save a figure with the *savefig* keyword to the plot file.  For example, type::

     >>> xml.plot_mass_fractions_vs_property('time', ['n', 'h1', 'he4', 'si28', 'ni56'], xscale = 'log', yscale = 'log', ylim = [1.e-10,1], xlabel = 'time (s)', ylabel = 'Mass Fractions', use_latex_names = True, xlim = [1.e-15, 100], savefig='x_vs_time.pdf')

The output is *x_vs_time.pdf*.  With :doc:`../installation/Docker`, you can
*docker cp* that file out of the container.

To get out of python, type::

     >>> exit()

To smooth out the plots, rerun the calculation but save data more frequently.
To do so, add the option ``--xml_steps 5`` to the execution command and repeat
all the steps.
