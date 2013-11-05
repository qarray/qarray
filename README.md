This program will read a input text file and convert the contents into a task array to be submitted to Grid Engine. 
The wrapper implements best practices for task array submissions within Grid Engine.  Each line of the input text file
should be a command that will be run as a task within the task array.  Multiple lines (commands) within the input file
can also be "chunked" or grouped together as a single task within the array.  For more information about task array 
refer to the -t and -tc options within the qsub man page.

This script assumes that you have the appropriate Grid Engine environment 
variables present in your shell environment.  This is typically accomplished by 
sourcing $SGE_ROOT/default/common/settings.(sh|csh).

qarray [options] -f {command file}

*Options:*<br>
<pre><code>-f     An input file containing a list of commands. </code></pre> 
<pre><code>-c     The number of input lines to chunk into a single job array element.</code></pre> 
<pre><code>-qo    A single-quoted string of additional options to be passed to qsub. </code></pre> 
<pre><code>-wd    The working directory for the job.  If not specified, this script will use the 
	   current working directory as the working directory for the job. </code></pre> 
<pre><code>-d     Select the level of verbosity. Default level is 0. </code></pre>
<pre><code>-help  Prints the usage information for this script. </code></pre>
<pre><code>-man  Prints the man page for this script. </code></pre>

*Required* <br>
Input text file with each line representing a individual command to be run as a task within a task array.

*Optional*  <br>
The number of input lines to chunk into a single job array element. The default value is 1.  This means that each line 
of the input file will represent a single task in the array.  If chunk size were set to 3 then every 3 lines in the 
input file would represent a single task in the array.

*Optional*  <br>
A single-quoted string of additional qsub options.  Note that the qsub options: -cwd, -r, -S, -sync and -wd are 
specified by other options within this script and need not be passed via the -qo argument.  For a complete list of all of 
the options that can be used with qsub run 'man qsub'.

*Optional* <br>
The working directory for the job.  This is set by specifying the qsub option of the same name: -wd. If the -wd is not
specified, this script will use the current working directory for the working directory for the job by passing the 
qsub option '-cwd' to qsub.

*Optional* <br>
The debug level for this script.  An explanation of the debug levels is as follows:

<pre><code>'0'	Do not print any statements for the qarray script to STDERR.  </code></pre> 
<pre><code>'1'	Print status information for the qarray script to STDERR. </code></pre> 

<div>
Delete all Grid Engine log files (*.o*, *.e*, *.po* and *.pe*) created for the job. The original job submit script and
master STDERR log file (if exists) will be preserved. </div>
