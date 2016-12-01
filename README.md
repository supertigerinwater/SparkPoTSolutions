# SparkPoTSolutions{
 "cells": [
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "# Lab 1 - Hello Spark\n",
    "This lab will introduce you to Apache Spark.  It will be written in Python and run in IBM's Data Science Experience environment through a Jupyter notebook.  While you work, it will be valuable to reference the [Apache Spark Documentation](http://spark.apache.org/docs/latest/programming-guide.html).  Since it is Python, be careful of whitespace!"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "## Step 1 - Working with Spark Context\n",
    "### Step 1.1 - Invoke the spark context: <i>version</i> will return the working version of Apache Spark<br><br>\n",
    " <div class=\"panel-group\" id=\"accordion-11\">\n",
    "  <div class=\"panel panel-default\">\n",
    "    <div class=\"panel-heading\">\n",
    "      <h4 class=\"panel-title\">\n",
    "        <a data-toggle=\"collapse\" data-parent=\"#accordion-11\" href=\"#collapse1-11\">\n",
    "        Hint 1</a>\n",
    "      </h4>\n",
    "    </div>\n",
    "    <div id=\"collapse1-11\" class=\"panel-collapse collapse\">\n",
    "      <div class=\"panel-body\">The spark context is automatically set in a Jupyter notebook.   It is called: sc</div>\n",
    "    </div>\n",
    "  </div>\n",
    "  <div class=\"panel panel-default\">\n",
    "    <div class=\"panel-heading\">\n",
    "      <h4 class=\"panel-title\">\n",
    "        <a data-toggle=\"collapse\" data-parent=\"#accordion-11\" href=\"#collapse2-11\">\n",
    "        Hint 2</a>\n",
    "      </h4>\n",
    "    </div>\n",
    "    <div id=\"collapse2-11\" class=\"panel-collapse collapse\">\n",
    "      <div class=\"panel-body\">Type:<br>&nbsp;&nbsp;&nbsp;&nbsp;sc.version</div>\n",
    "    </div>\n",
    "  </div>\n",
    "  <div class=\"panel panel-default\">\n",
    "    <div class=\"panel-heading\">\n",
    "      <h4 class=\"panel-title\">\n",
    "        <a data-toggle=\"collapse\" data-parent=\"#accordion-11\" href=\"#collapse3-11\">\n",
    "        Optional</a>\n",
    "      </h4>\n",
    "    </div>\n",
    "    <div id=\"collapse3-11\" class=\"panel-collapse collapse\">\n",
    "      <div class=\"panel-body\">Jupyter notebooks have command completion which can be invoked via the TAB key.<br>Type:<br>&nbsp;&nbsp;&nbsp;&nbsp;<i>sc.&lt;TAB&gt;</i><br>to see all the possible options within the Spark context</div>\n",
    "    </div>\n",
    "  </div>\n",
    "</div> "
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 1,
   "metadata": {
    "collapsed": false,
    "scrolled": true
   },
   "outputs": [
    {
     "data": {
      "text/plain": [
       "u'2.0.1'"
      ]
     },
     "execution_count": 1,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "#Step 1 - Check spark version\n",
    "sc.version"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "## Step 2 - Working with Resilient Distributed Datasets (RDD)\n",
    "\n",
    "### Step 2.1 - Create an RDD with numbers 1 to 10\n",
    "\n",
    "RDDs are the basic abstraction unit in Spark.   An RDD represents an immutable, partitioned, fault-tolerant collection of elements that can be operated on in parallel.<br>\n",
    "There are three ways to create an RDD: parallelizing an existing collection, referencing a dataset in an external storage system which offers a Hadoop InputFormat -- or transforming an existing RDD.<br>\n",
    "<br>\n",
    "Create an iterable or collection in your program with numbers 1 to 10 and then invoke the Spark Context's (sc) <i>parallelize()</i> method on it.<br>\n",
    "\n",
    " <div class=\"panel-group\" id=\"accordion-21\">\n",
    "  <div class=\"panel panel-default\">\n",
    "    <div class=\"panel-heading\">\n",
    "      <h4 class=\"panel-title\">\n",
    "        <a data-toggle=\"collapse\" data-parent=\"#accordion-21\" href=\"#collapse1-21\">\n",
    "        Hint 1</a>\n",
    "      </h4>\n",
    "    </div>\n",
    "    <div id=\"collapse1-21\" class=\"panel-collapse collapse\">\n",
    "      <div class=\"panel-body\">Type:<br>\n",
    "&nbsp;&nbsp;&nbsp;&nbsp;\n",
    "x = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]<br><br>\n",
    "Or we can try to be a little clever by typing:<br>\n",
    "&nbsp;&nbsp;&nbsp;&nbsp;\n",
    "x = range(1, 11)\n",
    "      </div>\n",
    "    </div>\n",
    "  </div>\n",
    "  <div class=\"panel panel-default\">\n",
    "    <div class=\"panel-heading\">\n",
    "      <h4 class=\"panel-title\">\n",
    "        <a data-toggle=\"collapse\" data-parent=\"#accordion-21\" href=\"#collapse2-21\">\n",
    "        Hint 2</a>\n",
    "      </h4>\n",
    "    </div>\n",
    "    <div id=\"collapse2-21\" class=\"panel-collapse collapse\">\n",
    "      <div class=\"panel-body\">Type:<br>\n",
    "&nbsp;&nbsp;&nbsp;&nbsp;\n",
    "x = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]<br>\n",
    "&nbsp;&nbsp;&nbsp;&nbsp; x_nbr_rdd = sc.parallelize(x)\n",
    "      </div>\n",
    "    </div>\n",
    "  </div>\n",
    "  <div class=\"panel panel-default\">\n",
    "    <div class=\"panel-heading\">\n",
    "      <h4 class=\"panel-title\">\n",
    "        <a data-toggle=\"collapse\" data-parent=\"#accordion-21\" href=\"#collapse3-21\">\n",
    "        Optional Advanced</a>\n",
    "      </h4>\n",
    "    </div>\n",
    "    <div id=\"collapse3-21\" class=\"panel-collapse collapse\">\n",
    "      <div class=\"panel-body\">An optional parameter to parallelize is the number of partitions to cut the dataset into.   Spark will run one task for each partition.   Typically you want 2-4 partitions for each CPU.   Normally, Spark will set it automatically, but you can control this by specifying it manually as a second parameter to the parallelize method.<br><br>\n",
    "You can obtain the partitions size by calling <i>&lt;RDD&gt;.getNumPartitions()</i><br>\n",
    "Try experimenting with different partitions sizes -- including ones higher than the number of values.   To see how the values are distributed use:<br><br>\n",
    "<i>\n",
    "def f(iterator):<br>\n",
    "    &nbsp;&nbsp;&nbsp;&nbsp;\n",
    "    count = 0<br>\n",
    "    &nbsp;&nbsp;&nbsp;&nbsp;\n",
    "    for value in iterator:<br>\n",
    "    &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;\n",
    "        count = count + 1<br>\n",
    "    &nbsp;&nbsp;&nbsp;&nbsp;\n",
    "    yield count<br>\n",
    "x_nbr_rdd.mapPartitions(f).collect()</i><br>\n",
    "      </div>\n",
    "    </div>\n",
    "  </div>\n",
    "</div> "
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 2,
   "metadata": {
    "collapsed": false
   },
   "outputs": [],
   "source": [
    "#Step 2.1 - Create RDD of numbers 1-10\n",
    "x = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]\n",
    "x_nbr_rdd = sc.parallelize(x) \n"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "### Step 2.2 - Return the first element<br><br>\n",
    " <div class=\"panel-group\" id=\"accordion-22\">\n",
    "  <div class=\"panel panel-default\">\n",
    "    <div class=\"panel-heading\">\n",
    "      <h4 class=\"panel-title\">\n",
    "        <a data-toggle=\"collapse\" data-parent=\"#accordion-22\" href=\"#collapse1-22\">\n",
    "        Hint 1</a>\n",
    "      </h4>\n",
    "    </div>\n",
    "    <div id=\"collapse1-22\" class=\"panel-collapse collapse\">\n",
    "      <div class=\"panel-body\">Use the <i>first()</i> method on the RDD to return the first element in an RDD.   You could also use the <i>take()</i> method with a parameter of 1.   first() and take(1) are equivalent.   Both will take the first element in the RDD's 0th partition.</div>\n",
    "    </div>\n",
    "  </div>\n",
    "  <div class=\"panel panel-default\">\n",
    "    <div class=\"panel-heading\">\n",
    "      <h4 class=\"panel-title\">\n",
    "        <a data-toggle=\"collapse\" data-parent=\"#accordion-22\" href=\"#collapse2-22\">\n",
    "        Hint 2</a>\n",
    "      </h4>\n",
    "    </div>\n",
    "    <div id=\"collapse2-22\" class=\"panel-collapse collapse\">\n",
    "      <div class=\"panel-body\">Type: <br>\n",
    "&nbsp;&nbsp;&nbsp;&nbsp;x_nbr_rdd.first()</div>\n",
    "    </div>\n",
    "  </div>\n",
    "</div> "
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 3,
   "metadata": {
    "collapsed": false
   },
   "outputs": [
    {
     "data": {
      "text/plain": [
       "1"
      ]
     },
     "execution_count": 3,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "#Step 2.2 - Return first element\n",
    "x_nbr_rdd.first()"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "### Step 2.3 - Return an array of the first five elements<br><br>\n",
    " <div class=\"panel-group\" id=\"accordion-23\">\n",
    "  <div class=\"panel panel-default\">\n",
    "    <div class=\"panel-heading\">\n",
    "      <h4 class=\"panel-title\">\n",
    "        <a data-toggle=\"collapse\" data-parent=\"#accordion-23\" href=\"#collapse1-23\">\n",
    "        Hint 1</a>\n",
    "      </h4>\n",
    "    </div>\n",
    "    <div id=\"collapse1-23\" class=\"panel-collapse collapse\">\n",
    "      <div class=\"panel-body\">Use the <i>take()</i> method</div>\n",
    "    </div>\n",
    "  </div>\n",
    "  <div class=\"panel panel-default\">\n",
    "    <div class=\"panel-heading\">\n",
    "      <h4 class=\"panel-title\">\n",
    "        <a data-toggle=\"collapse\" data-parent=\"#accordion-23\" href=\"#collapse2-23\">\n",
    "        Hint 2</a>\n",
    "      </h4>\n",
    "    </div>\n",
    "    <div id=\"collapse2-23\" class=\"panel-collapse collapse\">\n",
    "      <div class=\"panel-body\">Type:<br>\n",
    "&nbsp;&nbsp;&nbsp;&nbsp;x_nbr_rdd.take(5)</div>\n",
    "    </div>\n",
    "  </div>\n",
    "  <div class=\"panel panel-default\">\n",
    "    <div class=\"panel-heading\">\n",
    "      <h4 class=\"panel-title\">\n",
    "        <a data-toggle=\"collapse\" data-parent=\"#accordion-23\" href=\"#collapse3-23\">\n",
    "        Optional Advanced</a>\n",
    "      </h4>\n",
    "    </div>\n",
    "    <div id=\"collapse3-23\" class=\"panel-collapse collapse\">\n",
    "      <div class=\"panel-body\">How would you get the 5th-7th elements?   <i>take()</i> only accepts one parameter so <i>take(5,7)</i> will not work.<br>\n",
    "      </div>\n",
    "    </div>\n",
    "  </div>\n",
    "</div> \n"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 4,
   "metadata": {
    "collapsed": false
   },
   "outputs": [
    {
     "data": {
      "text/plain": [
       "[1, 2, 3, 4, 5]"
      ]
     },
     "execution_count": 4,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "#Step 2.3 - Return an array of the first five elements\n",
    "x_nbr_rdd.take(5)\n"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "### Step 2.4 - Perform a map transformation to increment each element of the array by 1.  The map function creates a new RDD by applying the function provided in the argument to each element.  For more information go to [Transformations](http://spark.apache.org/docs/latest/programming-guide.html#transformations)<br><br>\n",
    " <div class=\"panel-group\" id=\"accordion-24\">\n",
    "  <div class=\"panel panel-default\">\n",
    "    <div class=\"panel-heading\">\n",
    "      <h4 class=\"panel-title\">\n",
    "        <a data-toggle=\"collapse\" data-parent=\"#accordion-24\" href=\"#collapse1-24\">\n",
    "        Hint 1</a>\n",
    "      </h4>\n",
    "    </div>\n",
    "    <div id=\"collapse1-24\" class=\"panel-collapse collapse\">\n",
    "      <div class=\"panel-body\">Use the <i>map(func)</i> function on the RDD.   Map invokes function <i>func</i> on each element of the RDD.   You can also use a inline (or lambda) function.   The syntax for a lambda function is:<br>\n",
    "&nbsp;&nbsp;&nbsp;&nbsp;\n",
    "lambda &lt;var&gt;: &lt;myCode&gt;\n",
    "</div>\n",
    "    </div>\n",
    "  </div>\n",
    "  <div class=\"panel panel-default\">\n",
    "    <div class=\"panel-heading\">\n",
    "      <h4 class=\"panel-title\">\n",
    "        <a data-toggle=\"collapse\" data-parent=\"#accordion-24\" href=\"#collapse2-24\">\n",
    "        Hint 2</a>\n",
    "      </h4>\n",
    "    </div>\n",
    "    <div id=\"collapse2-24\" class=\"panel-collapse collapse\">\n",
    "      <div class=\"panel-body\">Type:<br>\n",
    "&nbsp;&nbsp;&nbsp;&nbsp;x_nbr_rdd_2 = x_nbr_rdd.map(lambda x: x+1)</div>\n",
    "    </div>\n",
    "  </div>\n",
    "  <div class=\"panel panel-default\">\n",
    "    <div class=\"panel-heading\">\n",
    "      <h4 class=\"panel-title\">\n",
    "        <a data-toggle=\"collapse\" data-parent=\"#accordion-24\" href=\"#collapse3-24\">\n",
    "        Optional Advanced</a>\n",
    "      </h4>\n",
    "    </div>\n",
    "    <div id=\"collapse3-24\" class=\"panel-collapse collapse\">\n",
    "      <div class=\"panel-body\">Write a function which increments the value by 1 and pass that function to map()</div>\n",
    "    </div>\n",
    "  </div>\n",
    "</div> \n"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 5,
   "metadata": {
    "collapsed": false
   },
   "outputs": [],
   "source": [
    "#Step 2.4 - Write your map function\n",
    "x_nbr_rdd_2 = x_nbr_rdd.map(lambda x: x+1)\n",
    "    \n",
    "#Optional Advanced\n",
    "#def f(var):\n",
    "#    return var + 1\n",
    "    \n",
    "#x_nbr_rdd_2 = x_nbr_rdd.map(f)"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "### Step 2.5 - Note that there was no result for step 2.4.  Why was this?  Take a look at all the elements of the new RDD.<br>\n",
    "Type:<br>\n",
    "&nbsp;&nbsp;&nbsp;&nbsp; x_nbr_rdd_2.collect()   "
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 6,
   "metadata": {
    "collapsed": false
   },
   "outputs": [
    {
     "data": {
      "text/plain": [
       "[2, 3, 4, 5, 6, 7, 8, 9, 10, 11]"
      ]
     },
     "execution_count": 6,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "#Step 2.5 - Check out the elements of the new RDD. Warning: Be careful with this in real life! Collect returns everything!\n",
    "\n",
    "x_nbr_rdd_2.collect()"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "### Step 2.6 - Create a new RDD with one string \"Hello Spark\" and print it by getting the first element.<br><br>\n",
    " <div class=\"panel-group\" id=\"accordion-26\">\n",
    "  <div class=\"panel panel-default\">\n",
    "    <div class=\"panel-heading\">\n",
    "      <h4 class=\"panel-title\">\n",
    "        <a data-toggle=\"collapse\" data-parent=\"#accordion-26\" href=\"#collapse1-26\">\n",
    "        Hint 1</a>\n",
    "      </h4>\n",
    "    </div>\n",
    "    <div id=\"collapse1-26\" class=\"panel-collapse collapse\">\n",
    "      <div class=\"panel-body\">Create a variable with the String \"Hello Spark\" and turn it into an RDD with the parallelize() function.   Remember that parallelize() is invoked from the Spark context!</div>\n",
    "    </div>\n",
    "  </div>\n",
    "  <div class=\"panel panel-default\">\n",
    "    <div class=\"panel-heading\">\n",
    "      <h4 class=\"panel-title\">\n",
    "        <a data-toggle=\"collapse\" data-parent=\"#accordion-26\" href=\"#collapse2-26\">\n",
    "        Hint 2</a>\n",
    "      </h4>\n",
    "    </div>\n",
    "    <div id=\"collapse2-26\" class=\"panel-collapse collapse\">\n",
    "      <div class=\"panel-body\">Type:<br>\n",
    "&nbsp;&nbsp;&nbsp;&nbsp; y = \"Hello Spark\"<br>\n",
    "&nbsp;&nbsp;&nbsp;&nbsp; y_str_rdd = sc.parallelize(y)<br>\n",
    "&nbsp;&nbsp;&nbsp;&nbsp; y_str_rdd.first()<br></div>\n",
    "    </div>\n",
    "  </div>\n",
    "  <div class=\"panel panel-default\">\n",
    "    <div class=\"panel-heading\">\n",
    "      <h4 class=\"panel-title\">\n",
    "        <a data-toggle=\"collapse\" data-parent=\"#accordion-26\" href=\"#collapse3-26\">\n",
    "        Optional Advanced</a>\n",
    "      </h4>\n",
    "    </div>\n",
    "    <div id=\"collapse3-26\" class=\"panel-collapse collapse\">\n",
    "      <div class=\"panel-body\">Why did getting the first element only print 'H' instead of \"Hello Spark\"?   What does <i>collect()</i> do?   Is there a way to have the first element be the full string instead of an individual character?</div>\n",
    "    </div>\n",
    "  </div>\n",
    "</div> "
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 7,
   "metadata": {
    "collapsed": false
   },
   "outputs": [
    {
     "data": {
      "text/plain": [
       "'Hello Spark'"
      ]
     },
     "execution_count": 7,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "#Step 2.6 - Create a string y, then turn it into an RDD\n",
    "y = [\"Hello Spark\"]\n",
    "foo = sc.parallelize(y)\n",
    "foo.first()"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "### Step 2.7 - Create a third RDD with the following strings and extract the first line.\n",
    "&nbsp;&nbsp;&nbsp;&nbsp;IBM Data Science Experience is built for enterprise-scale deployment.<br>\n",
    "&nbsp;&nbsp;&nbsp;&nbsp;Manage your data, your analytical assets, and your projects in a secured cloud environment.<br>\n",
    "&nbsp;&nbsp;&nbsp;&nbsp;When you create an account in the IBM Data Science Experience, we deploy for you a Spark as a Service instance to power your analysis and 5 GB of IBM Object Storage to store your data.<br><br>\n",
    " <div class=\"panel-group\" id=\"accordion-27\">\n",
    "  <div class=\"panel panel-default\">\n",
    "    <div class=\"panel-heading\">\n",
    "      <h4 class=\"panel-title\">\n",
    "        <a data-toggle=\"collapse\" data-parent=\"#accordion-27\" href=\"#collapse1-27\">\n",
    "        Hint 1</a>\n",
    "      </h4>\n",
    "    </div>\n",
    "    <div id=\"collapse1-27\" class=\"panel-collapse collapse\">\n",
    "      <div class=\"panel-body\">Use an array -- [] -- to contain all three strings.   Don't forget to enclose them in quotes!</div>\n",
    "    </div>\n",
    "  </div>\n",
    "  <div class=\"panel panel-default\">\n",
    "    <div class=\"panel-heading\">\n",
    "      <h4 class=\"panel-title\">\n",
    "        <a data-toggle=\"collapse\" data-parent=\"#accordion-27\" href=\"#collapse2-27\">\n",
    "        Hint 2</a>\n",
    "      </h4>\n",
    "    </div>\n",
    "    <div id=\"collapse2-27\" class=\"panel-collapse collapse\">\n",
    "      <div class=\"panel-body\">&nbsp;&nbsp;&nbsp;&nbsp; z = [ \"IBM Data Science Experience is built for enterprise-scale deployment.\", \"Manage your data, your analytical assets, and your projects in a secured cloud environment.\", \"When you create an account in the IBM Data Science Experience, we deploy for you a Spark as a Service instance to power your analysis and 5 GB of IBM Object Storage to store your data.\" ]<br>\n",
    "&nbsp;&nbsp;&nbsp;&nbsp; z_str_rdd = sc.parallelize(z)<br>\n",
    "&nbsp;&nbsp;&nbsp;&nbsp; z_str_rdd.first()      \n",
    "      </div>\n",
    "    </div>\n",
    "  </div>\n",
    "</div> "
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 8,
   "metadata": {
    "collapsed": false
   },
   "outputs": [
    {
     "data": {
      "text/plain": [
       "'IBM Data Science Experience is built for enterprise-scale deployment.'"
      ]
     },
     "execution_count": 8,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "#Step 2.7 - Create String RDD with many lines / entries, Extract first line\n",
    "z = [ \"IBM Data Science Experience is built for enterprise-scale deployment.\", \"Manage your data, your analytical assets, and your projects in a secured cloud environment.\", \"When you create an account in the IBM Data Science Experience, we deploy for you a Spark as a Service instance to power your analysis and 5 GB of IBM Object Storage to store your data.\" ]\n",
    "z_str_rdd = sc.parallelize(z)\n",
    "z_str_rdd.first()"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "### Step 2.8 - Count the number of entries in this RDD\n",
    "<br>\n",
    " <div class=\"panel-group\" id=\"accordion-28\">\n",
    "  <div class=\"panel panel-default\">\n",
    "    <div class=\"panel-heading\">\n",
    "      <h4 class=\"panel-title\">\n",
    "        <a data-toggle=\"collapse\" data-parent=\"#accordion-28\" href=\"#collapse1-28\">\n",
    "        Hint</a>\n",
    "      </h4>\n",
    "    </div>\n",
    "    <div id=\"collapse1-28\" class=\"panel-collapse collapse\">\n",
    "      <div class=\"panel-body\">Type:<br>\n",
    "&nbsp;&nbsp;&nbsp;&nbsp; z_str_rdd.count()<br></div>\n",
    "    </div>\n",
    "  </div>\n",
    "</div>"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 9,
   "metadata": {
    "collapsed": false
   },
   "outputs": [
    {
     "data": {
      "text/plain": [
       "3"
      ]
     },
     "execution_count": 9,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "#Step 2.8 - Count the number of entries in the RDD\n",
    "z_str_rdd.count()"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "### Step 2.9 - Inspect the elements of this RDD by collecting all the values\n",
    "<br>\n",
    " <div class=\"panel-group\" id=\"accordion-29\">\n",
    "  <div class=\"panel panel-default\">\n",
    "    <div class=\"panel-heading\">\n",
    "      <h4 class=\"panel-title\">\n",
    "        <a data-toggle=\"collapse\" data-parent=\"#accordion-29\" href=\"#collapse1-29\">\n",
    "        Hint</a>\n",
    "      </h4>\n",
    "    </div>\n",
    "    <div id=\"collapse1-29\" class=\"panel-collapse collapse\">\n",
    "      <div class=\"panel-body\">Type:<br>\n",
    "&nbsp;&nbsp;&nbsp;&nbsp;z_str_rdd.collect()<br></div>\n",
    "    </div>\n",
    "  </div>\n",
    "</div> "
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 10,
   "metadata": {
    "collapsed": false
   },
   "outputs": [
    {
     "data": {
      "text/plain": [
       "['IBM Data Science Experience is built for enterprise-scale deployment.',\n",
       " 'Manage your data, your analytical assets, and your projects in a secured cloud environment.',\n",
       " 'When you create an account in the IBM Data Science Experience, we deploy for you a Spark as a Service instance to power your analysis and 5 GB of IBM Object Storage to store your data.']"
      ]
     },
     "execution_count": 10,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "#Step 2.9 - Show all the entries in the RDD\n",
    "z_str_rdd.collect()"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "### Step 2.10 - Split all the entries in the RDD on the spaces.  Then print it out.  Pay careful attention to the new format.\n",
    "<br>\n",
    " <div class=\"panel-group\" id=\"accordion-210\">\n",
    "  <div class=\"panel panel-default\">\n",
    "    <div class=\"panel-heading\">\n",
    "      <h4 class=\"panel-title\">\n",
    "        <a data-toggle=\"collapse\" data-parent=\"#accordion-210\" href=\"#collapse1-210\">\n",
    "        Hint 1</a>\n",
    "      </h4>\n",
    "    </div>\n",
    "    <div id=\"collapse1-210\" class=\"panel-collapse collapse\">\n",
    "      <div class=\"panel-body\">To split on spaces, use the <a href=\"https://docs.python.org/2/library/stdtypes.html#string-methods\"><i>split()</i></a> function.</div>\n",
    "    </div>\n",
    "  </div>\n",
    "  <div class=\"panel panel-default\">\n",
    "    <div class=\"panel-heading\">\n",
    "      <h4 class=\"panel-title\">\n",
    "        <a data-toggle=\"collapse\" data-parent=\"#accordion-210\" href=\"#collapse2-210\">\n",
    "        Hint 2</a>\n",
    "      </h4>\n",
    "    </div>\n",
    "    <div id=\"collapse2-210\" class=\"panel-collapse collapse\">\n",
    "      <div class=\"panel-body\">Since you want to run on every line, use <i>map()</i> on the RDD and write a lambda function to call <i>split()</i></div>\n",
    "    </div>\n",
    "  </div>\n",
    "  <div class=\"panel panel-default\">\n",
    "    <div class=\"panel-heading\">\n",
    "      <h4 class=\"panel-title\">\n",
    "        <a data-toggle=\"collapse\" data-parent=\"#accordion-210\" href=\"#collapse3-210\">\n",
    "        Hint 3</a>\n",
    "      </h4>\n",
    "    </div>\n",
    "    <div id=\"collapse3-210\" class=\"panel-collapse collapse\">\n",
    "      <div class=\"panel-body\">Type: <br>\n",
    "&nbsp;&nbsp;&nbsp;&nbsp;z_str_rdd_split = z_str_rdd.map(lambda line: line.split(\" \"))<br>\n",
    "&nbsp;&nbsp;&nbsp;&nbsp;z_str_rdd_split.collect()<br><br>\n",
    "Question: Is there any difference between split(\" \") and split()?</div>\n",
    "    </div>\n",
    "  </div>\n",
    "</div> "
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 11,
   "metadata": {
    "collapsed": false,
    "scrolled": true
   },
   "outputs": [
    {
     "data": {
      "text/plain": [
       "[['IBM',\n",
       "  'Data',\n",
       "  'Science',\n",
       "  'Experience',\n",
       "  'is',\n",
       "  'built',\n",
       "  'for',\n",
       "  'enterprise-scale',\n",
       "  'deployment.'],\n",
       " ['Manage',\n",
       "  'your',\n",
       "  'data,',\n",
       "  'your',\n",
       "  'analytical',\n",
       "  'assets,',\n",
       "  'and',\n",
       "  'your',\n",
       "  'projects',\n",
       "  'in',\n",
       "  'a',\n",
       "  'secured',\n",
       "  'cloud',\n",
       "  'environment.'],\n",
       " ['When',\n",
       "  'you',\n",
       "  'create',\n",
       "  'an',\n",
       "  'account',\n",
       "  'in',\n",
       "  'the',\n",
       "  'IBM',\n",
       "  'Data',\n",
       "  'Science',\n",
       "  'Experience,',\n",
       "  'we',\n",
       "  'deploy',\n",
       "  'for',\n",
       "  'you',\n",
       "  'a',\n",
       "  'Spark',\n",
       "  'as',\n",
       "  'a',\n",
       "  'Service',\n",
       "  'instance',\n",
       "  'to',\n",
       "  'power',\n",
       "  'your',\n",
       "  'analysis',\n",
       "  'and',\n",
       "  '5',\n",
       "  'GB',\n",
       "  'of',\n",
       "  'IBM',\n",
       "  'Object',\n",
       "  'Storage',\n",
       "  'to',\n",
       "  'store',\n",
       "  'your',\n",
       "  'data.']]"
      ]
     },
     "execution_count": 11,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "#Step 2.10 - Perform a map transformation to split all entries in the RDD\n",
    "#Check out the entries in the new RDD\n",
    "z_str_rdd_split = z_str_rdd.map(lambda line: line.split())\n",
    "z_str_rdd_split.collect()"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "### Step 2.11 - Explore a new transformation: <a href=\"https://spark.apache.org/docs/1.6.0/api/python/pyspark#pyspark.RDD.flatMap\">flatMap</a>\n",
    "<br>\n",
    "We want to count the words in <b>all</b> the lines, but currently they are split by line.   We need to 'flatten' the line return values into one object.<br>\n",
    "flatMap will \"flatten\" all the elements of an RDD element into 0 or more output terms.<br><br>\n",
    " <div class=\"panel-group\" id=\"accordion-211\">\n",
    "  <div class=\"panel panel-default\">\n",
    "    <div class=\"panel-heading\">\n",
    "      <h4 class=\"panel-title\">\n",
    "        <a data-toggle=\"collapse\" data-parent=\"#accordion-211\" href=\"#collapse1-211\">\n",
    "        Hint 1</a>\n",
    "      </h4>\n",
    "    </div>\n",
    "    <div id=\"collapse1-211\" class=\"panel-collapse collapse\">\n",
    "      <div class=\"panel-body\"><i>flatmap()</i> parameters work the same way as in <i>map()</i></div>\n",
    "    </div>\n",
    "  </div>\n",
    "  <div class=\"panel panel-default\">\n",
    "    <div class=\"panel-heading\">\n",
    "      <h4 class=\"panel-title\">\n",
    "        <a data-toggle=\"collapse\" data-parent=\"#accordion-211\" href=\"#collapse2-211\">\n",
    "        Hint 2</a>\n",
    "      </h4>\n",
    "    </div>\n",
    "    <div id=\"collapse2-211\" class=\"panel-collapse collapse\">\n",
    "      <div class=\"panel-body\">Type:<br>\n",
    "&nbsp;&nbsp;&nbsp;&nbsp; z_str_rdd_split_flatmap = z_str_rdd.flatMap(lambda line: line.split(\" \"))<br>\n",
    "&nbsp;&nbsp;&nbsp;&nbsp; z_str_rdd_split_flatmap.collect()<br></div>\n",
    "    </div>\n",
    "  </div>\n",
    "  <div class=\"panel panel-default\">\n",
    "    <div class=\"panel-heading\">\n",
    "      <h4 class=\"panel-title\">\n",
    "        <a data-toggle=\"collapse\" data-parent=\"#accordion-211\" href=\"#collapse3-211\">\n",
    "        Optional Advanced</a>\n",
    "      </h4>\n",
    "    </div>\n",
    "    <div id=\"collapse3-211\" class=\"panel-collapse collapse\">\n",
    "      <div class=\"panel-body\">Use the replace() and lower() methods to remove all commas and periods then make everything lower-case</div>\n",
    "    </div>\n",
    "  </div>\n",
    "</div> "
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 12,
   "metadata": {
    "collapsed": false,
    "scrolled": true
   },
   "outputs": [
    {
     "data": {
      "text/plain": [
       "['ibm',\n",
       " 'data',\n",
       " 'science',\n",
       " 'experience',\n",
       " 'is',\n",
       " 'built',\n",
       " 'for',\n",
       " 'enterprise-scale',\n",
       " 'deployment',\n",
       " 'manage',\n",
       " 'your',\n",
       " 'data',\n",
       " 'your',\n",
       " 'analytical',\n",
       " 'assets',\n",
       " 'and',\n",
       " 'your',\n",
       " 'projects',\n",
       " 'in',\n",
       " 'a',\n",
       " 'secured',\n",
       " 'cloud',\n",
       " 'environment',\n",
       " 'when',\n",
       " 'you',\n",
       " 'create',\n",
       " 'an',\n",
       " 'account',\n",
       " 'in',\n",
       " 'the',\n",
       " 'ibm',\n",
       " 'data',\n",
       " 'science',\n",
       " 'experience',\n",
       " 'we',\n",
       " 'deploy',\n",
       " 'for',\n",
       " 'you',\n",
       " 'a',\n",
       " 'spark',\n",
       " 'as',\n",
       " 'a',\n",
       " 'service',\n",
       " 'instance',\n",
       " 'to',\n",
       " 'power',\n",
       " 'your',\n",
       " 'analysis',\n",
       " 'and',\n",
       " '5',\n",
       " 'gb',\n",
       " 'of',\n",
       " 'ibm',\n",
       " 'object',\n",
       " 'storage',\n",
       " 'to',\n",
       " 'store',\n",
       " 'your',\n",
       " 'data']"
      ]
     },
     "execution_count": 12,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "#Step 2.11 - Learn the difference between two transformations: map and flatMap.\n",
    "z_str_rdd_split_flatmap = z_str_rdd.flatMap(lambda line: line.split())\n",
    "z_str_rdd_split_flatmap.collect()\n",
    "#What do you notice? How are the outputs of 2.10 and 2.11 different?\n",
    "z_str_rdd_split_advanced = z_str_rdd_split_flatmap.map(lambda x: x.replace(',','').replace('.','').lower())\n",
    "z_str_rdd_split_advanced.collect()"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "### Step 2.12 - Augment each entry in the previous RDD with the number \"1\" to create pairs or tuples. The first element of the tuple will be the word and the second elements of the tuple will be the digit \"1\".  This is a common step in performing a count as we need values to sum.\n",
    "<br>\n",
    " <div class=\"panel-group\" id=\"accordion-212\">\n",
    "  <div class=\"panel panel-default\">\n",
    "    <div class=\"panel-heading\">\n",
    "      <h4 class=\"panel-title\">\n",
    "        <a data-toggle=\"collapse\" data-parent=\"#accordion-212\" href=\"#collapse1-212\">\n",
    "        Hint 1</a>\n",
    "      </h4>\n",
    "    </div>\n",
    "    <div id=\"collapse1-212\" class=\"panel-collapse collapse\">\n",
    "      <div class=\"panel-body\">Maps don't always have to perform calculations, they can just echo values as well.   Simply echo the value and a 1<br></div>\n",
    "    </div>\n",
    "  </div>\n",
    "  <div class=\"panel panel-default\">\n",
    "    <div class=\"panel-heading\">\n",
    "      <h4 class=\"panel-title\">\n",
    "        <a data-toggle=\"collapse\" data-parent=\"#accordion-212\" href=\"#collapse2-212\">\n",
    "        Hint 2</a>\n",
    "      </h4>\n",
    "    </div>\n",
    "    <div id=\"collapse2-212\" class=\"panel-collapse collapse\">\n",
    "      <div class=\"panel-body\">We need to create tuples which are values enclosed in parenthesis, so you'll need to enclose the value, 1 in parens.   For example: (x, 1)<br></div>\n",
    "    </div>\n",
    "  </div>\n",
    "  <div class=\"panel panel-default\">\n",
    "    <div class=\"panel-heading\">\n",
    "      <h4 class=\"panel-title\">\n",
    "        <a data-toggle=\"collapse\" data-parent=\"#accordion-212\" href=\"#collapse3-212\">\n",
    "        Hint 3</a>\n",
    "      </h4>\n",
    "    </div>\n",
    "    <div id=\"collapse3-212\" class=\"panel-collapse collapse\">\n",
    "      <div class=\"panel-body\">Type:<br>\n",
    "&nbsp;&nbsp;&nbsp;&nbsp; countWords = z_str_rdd_split_flatmap.map(lambda word:(word,1))<br>\n",
    "&nbsp;&nbsp;&nbsp;&nbsp; countWords.collect()<br></div>\n",
    "    </div>\n",
    "  </div>\n",
    "</div> "
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 13,
   "metadata": {
    "collapsed": false
   },
   "outputs": [
    {
     "data": {
      "text/plain": [
       "[('IBM', 1),\n",
       " ('Data', 1),\n",
       " ('Science', 1),\n",
       " ('Experience', 1),\n",
       " ('is', 1),\n",
       " ('built', 1),\n",
       " ('for', 1),\n",
       " ('enterprise-scale', 1),\n",
       " ('deployment.', 1),\n",
       " ('Manage', 1),\n",
       " ('your', 1),\n",
       " ('data,', 1),\n",
       " ('your', 1),\n",
       " ('analytical', 1),\n",
       " ('assets,', 1),\n",
       " ('and', 1),\n",
       " ('your', 1),\n",
       " ('projects', 1),\n",
       " ('in', 1),\n",
       " ('a', 1),\n",
       " ('secured', 1),\n",
       " ('cloud', 1),\n",
       " ('environment.', 1),\n",
       " ('When', 1),\n",
       " ('you', 1),\n",
       " ('create', 1),\n",
       " ('an', 1),\n",
       " ('account', 1),\n",
       " ('in', 1),\n",
       " ('the', 1),\n",
       " ('IBM', 1),\n",
       " ('Data', 1),\n",
       " ('Science', 1),\n",
       " ('Experience,', 1),\n",
       " ('we', 1),\n",
       " ('deploy', 1),\n",
       " ('for', 1),\n",
       " ('you', 1),\n",
       " ('a', 1),\n",
       " ('Spark', 1),\n",
       " ('as', 1),\n",
       " ('a', 1),\n",
       " ('Service', 1),\n",
       " ('instance', 1),\n",
       " ('to', 1),\n",
       " ('power', 1),\n",
       " ('your', 1),\n",
       " ('analysis', 1),\n",
       " ('and', 1),\n",
       " ('5', 1),\n",
       " ('GB', 1),\n",
       " ('of', 1),\n",
       " ('IBM', 1),\n",
       " ('Object', 1),\n",
       " ('Storage', 1),\n",
       " ('to', 1),\n",
       " ('store', 1),\n",
       " ('your', 1),\n",
       " ('data.', 1)]"
      ]
     },
     "execution_count": 13,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "#Step 2.12 - Create pairs or tuple RDD and print it.\n",
    "countWords = z_str_rdd_split_flatmap.map(lambda word:(word, 1))\n",
    "countWords.collect()"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "### Step 2.13 Now we have above what is known as a [Pair RDD](http://spark.apache.org/docs/latest/api/scala/index.html#org.apache.spark.rdd.PairRDDFunctions). Each entry in the RDD has a KEY and a VALUE.<br>\n",
    "The KEY is the word (Light, of, the, ...) and the value is the number \"1\".  \n",
    "We can now AGGREGATE this RDD by summing up all the values BY KEY<br><br>\n",
    " <div class=\"panel-group\" id=\"accordion-213\">\n",
    "  <div class=\"panel panel-default\">\n",
    "    <div class=\"panel-heading\">\n",
    "      <h4 class=\"panel-title\">\n",
    "        <a data-toggle=\"collapse\" data-parent=\"#accordion-213\" href=\"#collapse1-213\">\n",
    "        Hint 1</a>\n",
    "      </h4>\n",
    "    </div>\n",
    "    <div id=\"collapse1-213\" class=\"panel-collapse collapse in\">\n",
    "      <div class=\"panel-body\">We want to sum all values by key in the key-value pairs.  The generic function to do this is <i>reduceByKey(func)</i>:<br>\n",
    "      &nbsp;&nbsp;&nbsp;&nbsp;When called on a dataset of (K [Key], V [Value]) pairs, returns a dataset of (K, V) pairs where the values for each key are aggregated using the given reduce function func, which must be of type (V,V) => V.<br><br>Which means func(v1, v2) runs across all values for a specific key.  Think of v1 as the output (initialized as 0 or \"\") and v2 as the iterated value over each value in the set with the same key.  With each iterated value, v1 is updated.<br>\n",
    "      Use a lambda function to sum up the values just as you wrote for <i>map()</i></div>\n",
    "    </div>\n",
    "  </div>\n",
    "  <div class=\"panel panel-default\">\n",
    "    <div class=\"panel-heading\">\n",
    "      <h4 class=\"panel-title\">\n",
    "        <a data-toggle=\"collapse\" data-parent=\"#accordion-213\" href=\"#collapse2-213\">\n",
    "         Hint 2</a>\n",
    "      </h4>\n",
    "    </div>\n",
    "    <div id=\"collapse2-213\" class=\"panel-collapse collapse\">\n",
    "      <div class=\"panel-body\">Type:<br>\n",
    "&nbsp;&nbsp;&nbsp;&nbsp;countWords2 = countWords.reduceByKey(lambda x,y: x+y)<br>\n",
    "&nbsp;&nbsp;&nbsp;&nbsp;countWords2.collect()<br></div>\n",
    "    </div>\n",
    "  </div>\n",
    "  <div class=\"panel panel-default\">\n",
    "    <div class=\"panel-heading\">\n",
    "      <h4 class=\"panel-title\">\n",
    "        <a data-toggle=\"collapse\" data-parent=\"#accordion-213\" href=\"#collapse3-213\">\n",
    "        Optional Advanced</a>\n",
    "      </h4>\n",
    "    </div>\n",
    "    <div id=\"collapse3-213\" class=\"panel-collapse collapse\">\n",
    "      <div class=\"panel-body\">Sort the results by the count.   You could call <i>sortByKey()</i> on the result, but it works on the key....<br>\n",
    "      Also, while the function used in <i>map()</i> has only one parameter, when working with Pair RDDs, that parameter is an array of two values....\n",
    "      </div>\n",
    "    </div>\n",
    "  </div>\n",
    "</div> \n"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 14,
   "metadata": {
    "collapsed": false,
    "scrolled": true
   },
   "outputs": [
    {
     "data": {
      "text/plain": [
       "[(5, 'your'),\n",
       " (3, 'a'),\n",
       " (3, 'IBM'),\n",
       " (2, 'and'),\n",
       " (2, 'for'),\n",
       " (2, 'you'),\n",
       " (2, 'Data'),\n",
       " (2, 'Science'),\n",
       " (2, 'to'),\n",
       " (2, 'in'),\n",
       " (1, 'enterprise-scale'),\n",
       " (1, 'Service'),\n",
       " (1, 'is'),\n",
       " (1, 'Storage'),\n",
       " (1, 'assets,'),\n",
       " (1, 'as'),\n",
       " (1, 'cloud'),\n",
       " (1, 'secured'),\n",
       " (1, '5'),\n",
       " (1, 'store'),\n",
       " (1, 'we'),\n",
       " (1, 'power'),\n",
       " (1, 'When'),\n",
       " (1, 'Experience'),\n",
       " (1, 'Spark'),\n",
       " (1, 'projects'),\n",
       " (1, 'account'),\n",
       " (1, 'analysis'),\n",
       " (1, 'deployment.'),\n",
       " (1, 'analytical'),\n",
       " (1, 'the'),\n",
       " (1, 'create'),\n",
       " (1, 'data,'),\n",
       " (1, 'data.'),\n",
       " (1, 'instance'),\n",
       " (1, 'Experience,'),\n",
       " (1, 'Manage'),\n",
       " (1, 'an'),\n",
       " (1, 'environment.'),\n",
       " (1, 'Object'),\n",
       " (1, 'GB'),\n",
       " (1, 'deploy'),\n",
       " (1, 'of'),\n",
       " (1, 'built')]"
      ]
     },
     "execution_count": 14,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "#Step 2.13 - Check out the results of the aggregation\n",
    "countWords2 = countWords.reduceByKey(lambda x,y: x+y)\n",
    "countWords3 = countWords2.map(lambda x: (x[1],x[0]))\n",
    "countWords3.sortByKey(False).collect()"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "## Step 3 - Reading a file and counting words\n",
    "### Step 3.1 - Read the Apache Spark README.md file from Github.  The ! allows you to embed file system commands\n",
    "<br>\n",
    "We remove README.md in case there was an updated version -- but also for another reason you will discover in Lab 2<br><br>\n",
    "Type:<br>\n",
    "\n",
    "&nbsp;&nbsp;&nbsp;&nbsp;!rm README.md* -f<br>\n",
    "&nbsp;&nbsp;&nbsp;&nbsp;!wget https://raw.githubusercontent.com/apache/spark/master/README.md<br>\n"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 15,
   "metadata": {
    "collapsed": false,
    "scrolled": true
   },
   "outputs": [
    {
     "name": "stdout",
     "output_type": "stream",
     "text": [
      "--2016-11-16 14:15:30--  https://raw.githubusercontent.com/apache/spark/master/README.md\n",
      "Resolving raw.githubusercontent.com (raw.githubusercontent.com)... 151.101.48.133\n",
      "Connecting to raw.githubusercontent.com (raw.githubusercontent.com)|151.101.48.133|:443... connected.\n",
      "HTTP request sent, awaiting response... 200 OK\n",
      "Length: 4034 (3.9K) [text/plain]\n",
      "Saving to: 'README.md'\n",
      "\n",
      "100%[======================================>] 4,034       --.-K/s   in 0s      \n",
      "\n",
      "2016-11-16 14:15:30 (29.9 MB/s) - 'README.md' saved [4034/4034]\n",
      "\n"
     ]
    }
   ],
   "source": [
    "#Step 3.1 - Pull data file into workbench\n",
    "!rm README.md* -f\n",
    "!wget https://raw.githubusercontent.com/apache/spark/master/README.md"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "### Step 3.2 - Create an RDD by reading from the local filesystem and count the number of lines  Here is the [textfile()](http://spark.apache.org/docs/latest/api/python/pyspark.html?highlight=textfile#pyspark.SparkContext.textFile) documentation.<br><br>\n",
    " <div class=\"panel-group\" id=\"accordion-32\">\n",
    "  <div class=\"panel panel-default\">\n",
    "    <div class=\"panel-heading\">\n",
    "      <h4 class=\"panel-title\">\n",
    "        <a data-toggle=\"collapse\" data-parent=\"#accordion-32\" href=\"#collapse1-32\">\n",
    "        Hint 1</a>\n",
    "      </h4>\n",
    "    </div>\n",
    "    <div id=\"collapse1-32\" class=\"panel-collapse collapse\">\n",
    "      <div class=\"panel-body\">README.md has been loaded into local storage so there is no path needed.   <i>textFile()</i> returns an RDD -- you do not have to parallelize the result.</div>\n",
    "    </div>\n",
    "  </div>\n",
    "  <div class=\"panel panel-default\">\n",
    "    <div class=\"panel-heading\">\n",
    "      <h4 class=\"panel-title\">\n",
    "        <a data-toggle=\"collapse\" data-parent=\"#accordion-32\" href=\"#collapse2-32\">\n",
    "        Hint 2</a>\n",
    "      </h4>\n",
    "    </div>\n",
    "    <div id=\"collapse2-32\" class=\"panel-collapse collapse\">\n",
    "      <div class=\"panel-body\">Type:<br>\n",
    "&nbsp;&nbsp;&nbsp;&nbsp;textfile_rdd = sc.textFile(\"README.md\")<br>\n",
    "&nbsp;&nbsp;&nbsp;&nbsp;textfile_rdd.count()<br></div>\n",
    "    </div>\n",
    "  </div>\n",
    "  <div class=\"panel panel-default\">\n",
    "    <div class=\"panel-heading\">\n",
    "      <h4 class=\"panel-title\">\n",
    "        <a data-toggle=\"collapse\" data-parent=\"#accordion-32\" href=\"#collapse3-32\">\n",
    "        Optional Advanced 3</a>\n",
    "      </h4>\n",
    "    </div>\n",
    "    <div id=\"collapse3-32\" class=\"panel-collapse collapse\">\n",
    "      <div class=\"panel-body\">By default, <i>textFile()</i> uses UTF-8 format.   Read the file as UNICODE.</div>\n",
    "    </div>\n",
    "  </div>\n",
    "</div> \n"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 16,
   "metadata": {
    "collapsed": false
   },
   "outputs": [
    {
     "data": {
      "text/plain": [
       "104"
      ]
     },
     "execution_count": 16,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "#Step 3.2 - Create RDD from data file\n",
    "textfile_rdd = sc.textFile(\"README.md\")\n",
    "textfile_rdd.count()\n",
    "\n",
    "#Optional Advanced 3\n",
    "#textfile_rdd = sc.textFile(\"README.md\", None, True)\n"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "### Step 3.3 - Filter out lines that contain \"Spark\". This will be achieved using the [filter](http://spark.apache.org/docs/latest/api/python/pyspark.html?highlight=filter#pyspark.RDD.filter) transformation.  Python allows us to use the 'in' syntax to search strings.<br>\n",
    "We will also take a look at the first line in the newly filtered RDD. <br><br>\n",
    " <div class=\"panel-group\" id=\"accordion-33\">\n",
    "  <div class=\"panel panel-default\">\n",
    "    <div class=\"panel-heading\">\n",
    "      <h4 class=\"panel-title\">\n",
    "        <a data-toggle=\"collapse\" data-parent=\"#accordion-33\" href=\"#collapse1-33\">\n",
    "        Hint 1</a>\n",
    "      </h4>\n",
    "    </div>\n",
    "    <div id=\"collapse1-33\" class=\"panel-collapse collapse\">\n",
    "      <div class=\"panel-body\"><i>filter()</i>, just like <i>map()</i> can take a lambda function as its input</div>\n",
    "    </div>\n",
    "  </div>\n",
    "  <div class=\"panel panel-default\">\n",
    "    <div class=\"panel-heading\">\n",
    "      <h4 class=\"panel-title\">\n",
    "        <a data-toggle=\"collapse\" data-parent=\"#accordion-33\" href=\"#collapse2-33\">\n",
    "        Hint 2</a>\n",
    "      </h4>\n",
    "    </div>\n",
    "    <div id=\"collapse2-33\" class=\"panel-collapse collapse\">\n",
    "      <div class=\"panel-body\">Type:<br>\n",
    "&nbsp;&nbsp;&nbsp;&nbsp;Spark_lines = textfile_rdd.filter(lambda line: \"Spark\" in line)<br>\n",
    "&nbsp;&nbsp;&nbsp;&nbsp;Spark_lines.first()<br></div>\n",
    "    </div>\n",
    "  </div>\n",
    "  <div class=\"panel panel-default\">\n",
    "    <div class=\"panel-heading\">\n",
    "      <h4 class=\"panel-title\">\n",
    "        <a data-toggle=\"collapse\" data-parent=\"#accordion-33\" href=\"#collapse3-33\">\n",
    "        Advanced Optional</a>\n",
    "      </h4>\n",
    "    </div>\n",
    "    <div id=\"collapse3-33\" class=\"panel-collapse collapse\">\n",
    "      <div class=\"panel-body\">There are 19 lines which contain the word \"Spark\".   Find all lines which contain it when case-insensitive<br></div>\n",
    "    </div>\n",
    "  </div>\n",
    "</div> "
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 17,
   "metadata": {
    "collapsed": false
   },
   "outputs": [],
   "source": [
    "#Step 3.3 - Filter for only lines with word Spark\n",
    "Spark_lines = textfile_rdd.filter(lambda line: \"spark\" in line.lower())"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "### Step 3.4 - Print the number of Spark lines in this filtered RDD out of the total number and print the result as a concatenated string.<br><br>\n",
    " <div class=\"panel-group\" id=\"accordion-34\">\n",
    "  <div class=\"panel panel-default\">\n",
    "    <div class=\"panel-heading\">\n",
    "      <h4 class=\"panel-title\">\n",
    "        <a data-toggle=\"collapse\" data-parent=\"#accordion-34\" href=\"#collapse1-34\">\n",
    "        Hint 1</a>\n",
    "      </h4>\n",
    "    </div>\n",
    "    <div id=\"collapse1-34\" class=\"panel-collapse collapse\">\n",
    "      <div class=\"panel-body\">The <i>print()</i> statement prints to the console.  (Note: be careful on a cluster because a print on a distributed machine will not be seen).  You can cast integers to string by using the <i>str()</i> method.</div>\n",
    "    </div>\n",
    "  </div>\n",
    "  <div class=\"panel panel-default\">\n",
    "    <div class=\"panel-heading\">\n",
    "      <h4 class=\"panel-title\">\n",
    "        <a data-toggle=\"collapse\" data-parent=\"#accordion-34\" href=\"#collapse2-34\">\n",
    "        Hint 2</a>\n",
    "      </h4>\n",
    "    </div>\n",
    "    <div id=\"collapse2-34\" class=\"panel-collapse collapse\">\n",
    "      <div class=\"panel-body\">Strings can be concatenated together with the + sign.   You can mark a statement as spanning multiple lines by putting a \\ at the end of the line.</div>\n",
    "    </div>\n",
    "  </div>\n",
    "  <div class=\"panel panel-default\">\n",
    "    <div class=\"panel-heading\">\n",
    "      <h4 class=\"panel-title\">\n",
    "        <a data-toggle=\"collapse\" data-parent=\"#accordion-34\" href=\"#collapse3-34\">\n",
    "        Hint 3</a>\n",
    "      </h4>\n",
    "    </div>\n",
    "    <div id=\"collapse3-34\" class=\"panel-collapse collapse\">\n",
    "      <div class=\"panel-body\">Type:<br>\n",
    "&nbsp;&nbsp;&nbsp;&nbsp;print \"The file README.md has \" + str(Spark_lines.count()) + \\<br>\n",
    "&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;\" of \" + str(textfile_rdd.count()) + \\<br>\n",
    "&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;\" lines with the word Spark in it.\"<br></div>\n",
    "    </div>\n",
    "  </div>\n",
    "</div> "
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 18,
   "metadata": {
    "collapsed": false
   },
   "outputs": [
    {
     "name": "stdout",
     "output_type": "stream",
     "text": [
      "The file README.md has 30 of 104 lines with the word Spark in it.\n"
     ]
    }
   ],
   "source": [
    "#Step 3.4 - count the number of lines\n",
    "print \"The file README.md has \" + str(Spark_lines.count()) + \\\n",
    "        \" of \" + str(textfile_rdd.count()) + \\\n",
    "        \" lines with the word Spark in it.\""
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "### Step 3.5 - Now count the number of times the word Spark appears in the original text, not just the number of lines that contain it.\n",
    "Looking back at previous exercises, you will need to: <br>\n",
    "&nbsp;&nbsp;&nbsp;&nbsp;1 - Execute a flatMap transformation on the original RDD Spark_lines and split on white space.<br>\n",
    "&nbsp;&nbsp;&nbsp;&nbsp;2 - Filter out all instances of the word Spark<br>\n",
    "&nbsp;&nbsp;&nbsp;&nbsp;3 - Count all instances<br>\n",
    "&nbsp;&nbsp;&nbsp;&nbsp;4 - Print the total count<br><br>\n",
    " <div class=\"panel-group\" id=\"accordion-35\">\n",
    "  <div class=\"panel panel-default\">\n",
    "    <div class=\"panel-heading\">\n",
    "      <h4 class=\"panel-title\">\n",
    "        <a data-toggle=\"collapse\" data-parent=\"#accordion-35\" href=\"#collapse1-35\">\n",
    "        Hint 1</a>\n",
    "      </h4>\n",
    "    </div>\n",
    "    <div id=\"collapse1-35\" class=\"panel-collapse collapse\">\n",
    "      <div class=\"panel-body\"><i>str</i> not in <i>string</i> is how to filter out</div>\n",
    "    </div>\n",
    "  </div>\n",
    "  <div class=\"panel panel-default\">\n",
    "    <div class=\"panel-heading\">\n",
    "      <h4 class=\"panel-title\">\n",
    "        <a data-toggle=\"collapse\" data-parent=\"#accordion-35\" href=\"#collapse2-35\">\n",
    "        Hint 2</a>\n",
    "      </h4>\n",
    "    </div>\n",
    "    <div id=\"collapse2-35\" class=\"panel-collapse collapse\">\n",
    "      <div class=\"panel-body\">flatMapRDD = textfile_rdd.flatMap(lambda line: line.split())<br>\n",
    "      flatMapRDDFilter = flatMapRDD.filter(lambda line: \"Spark\" not in line)<br>\n",
    "      flatMapRDDFilterCount = flatMapRDDFilter.count()<br>\n",
    "      print flatMapRDDFilterCount<br>\n",
    "      </div>\n",
    "    </div>\n",
    "  </div>\n",
    "  <div class=\"panel panel-default\">\n",
    "    <div class=\"panel-heading\">\n",
    "      <h4 class=\"panel-title\">\n",
    "        <a data-toggle=\"collapse\" data-parent=\"#accordion-35\" href=\"#collapse3-35\">\n",
    "        Optional Advanced</a>\n",
    "      </h4>\n",
    "    </div>\n",
    "    <div id=\"collapse3-35\" class=\"panel-collapse collapse\">\n",
    "      <div class=\"panel-body\">Put the entire statement on one line and make the filter case-insensitive.</div>\n",
    "    </div>\n",
    "  </div>\n",
    "</div> "
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 19,
   "metadata": {
    "collapsed": false
   },
   "outputs": [
    {
     "data": {
      "text/plain": [
       "[(u'Spark', 15)]"
      ]
     },
     "execution_count": 19,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "#Step 3.5 - Count the number of instances of\"Spark\"\n",
    "#flatMapRDD = textfile_rdd.flatMap(lambda line: line.split())\n",
    "#flatMapFiltered = flatMapRDD.filter(lambda x: x==\"Spark\")\n",
    "#flatMapFilteredMapped = flatMapFiltered.map(lambda x: (x,1))\n",
    "#FMFMReduced = flatMapFilteredMapped.reduceByKey(lambda x,y: x+y)\n",
    "#print FMFMReduced.collect()\n",
    "\n",
    "#Optional Advanced\n",
    "textfile_rdd.flatMap(lambda line: line.split()).filter(lambda x: x.lower()==\"spark\").map(lambda x: (x,1)).reduceByKey(lambda x,y: x+y).collect()"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "## Step 4 - Perform analysis on a data file\n",
    "This part is a little more open ended and there are a few ways to complete it.  Scroll up to previous examples for some guidance.  You will download a data file, transform the data, and then average the prices.  The data file will be a sample of tech stock prices over six days. <br>\n",
    "\n",
    "Data Location: https://raw.githubusercontent.com/JosephKambourakisIBM/SparkPoT/master/StockPrices.csv<br>\n",
    "The data file is a csv<br>\n",
    "Here is a sample of the file:<br>\n",
    "&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;\"IBM\",\"159.720001\" ,\"159.399994\" ,\"158.880005\",\"159.539993\", \"159.550003\", \"160.350006\""
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 20,
   "metadata": {
    "collapsed": false,
    "scrolled": true
   },
   "outputs": [
    {
     "name": "stdout",
     "output_type": "stream",
     "text": [
      "--2016-11-16 14:15:32--  https://raw.githubusercontent.com/JosephKambourakisIBM/SparkPoT/master/StockPrices.csv\n",
      "Resolving raw.githubusercontent.com (raw.githubusercontent.com)... 151.101.48.133\n",
      "Connecting to raw.githubusercontent.com (raw.githubusercontent.com)|151.101.48.133|:443... connected.\n",
      "HTTP request sent, awaiting response... 200 OK\n",
      "Length: 244 [text/plain]\n",
      "Saving to: 'StockPrices.csv'\n",
      "\n",
      "100%[======================================>] 244         --.-K/s   in 0s      \n",
      "\n",
      "2016-11-16 14:15:32 (54.9 MB/s) - 'StockPrices.csv' saved [244/244]\n",
      "\n"
     ]
    }
   ],
   "source": [
    "#Step 4.1 - Delete the file if it exists, download a new copy and load it into an RDD\n",
    "!rm StockPrices.csv -f\n",
    "!wget https://raw.githubusercontent.com/JosephKambourakisIBM/SparkPoT/master/StockPrices.csv\n",
    "    \n",
    "SP = sc.textFile(\"StockPrices.csv\")"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 21,
   "metadata": {
    "collapsed": false
   },
   "outputs": [
    {
     "data": {
      "text/plain": [
       "[(u'IBM', 159.720001, 159.399994, 158.880005, 159.539993, 159.550003),\n",
       " (u'MSFT', 58.099998, 57.889999, 57.459999, 57.59, 57.669998),\n",
       " (u'AAPL', 106.82, 106.0, 106.099998, 106.730003, 107.730003),\n",
       " (u'ORCL', 41.310001, 41.310001, 41.220001, 41.16, 41.25)]"
      ]
     },
     "execution_count": 21,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "#Step 4.2 - Transform the data to extract the stock ticker symbol and the prices.  \n",
    "SP_mapped = SP.map(lambda line: line.split(','))\n",
    "SP_Keyed = SP_mapped.map(lambda x: (x[0], float(x[1]), float(x[2]), float(x[3]), float(x[4]), float(x[5])))\n",
    "SP_Keyed.collect()"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 22,
   "metadata": {
    "collapsed": false
   },
   "outputs": [
    {
     "data": {
      "text/plain": [
       "[(u'IBM', 159.4179992),\n",
       " (u'MSFT', 57.7419988),\n",
       " (u'AAPL', 106.6760008),\n",
       " (u'ORCL', 41.2500006)]"
      ]
     },
     "execution_count": 22,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "#Step 4.3 - Compute the averages and print them for each symbol.\n",
    "SP_Mean = SP_Keyed.map(lambda x: (x[0], (x[1]+x[2]+ x[3]+ x[4]+x[5])/5)) #There are other ways to do this such as importing a mean function from numpy\n",
    "SP_Mean.collect()\n",
    "\n",
    "#Using a mean function\n",
    "#import numpy\n",
    "#SP_Mean = SP_Keyed.map(lambda x: (x[0], numpy.mean([x[1],x[2], x[3], x[4], x[5]]))) \n",
    "#SP_Mean.collect()"
   ]
  }
 ],
 "metadata": {
  "kernelspec": {
   "display_name": "Python 2 with Spark 2.0",
   "language": "python",
   "name": "python2-spark20"
  },
  "language_info": {
   "codemirror_mode": {
    "name": "ipython",
    "version": 2
   },
   "file_extension": ".py",
   "mimetype": "text/x-python",
   "name": "python",
   "nbconvert_exporter": "python",
   "pygments_lexer": "ipython2",
   "version": "2.7.11"
  }
 },
 "nbformat": 4,
 "nbformat_minor": 0
}
{
 "cells": [
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "# Lab 2 - Spark SQL\n",
    "![image](https://hadoopi.files.wordpress.com/2014/10/screen-shot-2014-10-25-at-14-29-50.png?w=597&h=222)\n",
    "\n",
    "This lab will show you how to work with the [SparkSQL](http://spark.apache.org/sql/) library.  It's meant to be self-guided, but don't hesitate to ask your presentor for help.  "
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "## Step 1 - Getting started: Create a [Spark Session](http://spark.apache.org/docs/latest/sql-programming-guide.html#starting-point-sparksession)\n",
    "<br>\n",
    " <div class=\"panel-group\" id=\"accordion-1\">\n",
    "  <div class=\"panel panel-default\">\n",
    "    <div class=\"panel-heading\">\n",
    "      <h4 class=\"panel-title\">\n",
    "        <a data-toggle=\"collapse\" data-parent=\"#accordion-1\" href=\"#collapse1-1\">\n",
    "        Hint 1</a>\n",
    "      </h4>\n",
    "    </div>\n",
    "    <div id=\"collapse1-1\" class=\"panel-collapse collapse\">\n",
    "      <div class=\"panel-body\"><i>SparkSession</i> is not included by default.   You need to import it from <i>pyspark.sql</i></div>\n",
    "    </div>\n",
    "  </div>\n",
    "  <div class=\"panel panel-default\">\n",
    "    <div class=\"panel-heading\">\n",
    "      <h4 class=\"panel-title\">\n",
    "        <a data-toggle=\"collapse\" data-parent=\"#accordion-1\" href=\"#collapse2-1\">\n",
    "        Hint 2</a>\n",
    "      </h4>\n",
    "    </div>\n",
    "    <div id=\"collapse2-1\" class=\"panel-collapse collapse\">\n",
    "      <div class=\"panel-body\"><i>SparkSession</i> needs the builder method.</div>\n",
    "    </div>\n",
    "  </div>\n",
    "  <div class=\"panel panel-default\">\n",
    "    <div class=\"panel-heading\">\n",
    "      <h4 class=\"panel-title\">\n",
    "        <a data-toggle=\"collapse\" data-parent=\"#accordion-1\" href=\"#collapse3-1\">\n",
    "        Hint 3</a>\n",
    "      </h4>\n",
    "    </div>\n",
    "    <div id=\"collapse3-1\" class=\"panel-collapse collapse\">\n",
    "      <div class=\"panel-body\">Type:<br>\n",
    "\n",
    "from pyspark.sql import SparkSession<br>\n",
    "spark = SparkSession.builder.getOrCreate()<br></div>\n",
    "    </div>\n",
    "  </div>\n",
    "</div> \n"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 1,
   "metadata": {
    "collapsed": false
   },
   "outputs": [],
   "source": [
    "#Import the SparkSQL library and connect to the current Spark context\n",
    "from pyspark.sql import SparkSession\n",
    "spark = SparkSession.builder.getOrCreate()"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "## Step 2 - Download a JSON Recordset to work with\n",
    "Let's download the data, we can run commands on the console of the server (or docker image) that the notebook environment is using. To do so we simply put a \"!\" in front of the command that we want to run. For example:\n",
    "\n",
    "!pwd\n",
    "\n",
    "To get the data we will download a file to the environment. Simple run these two commands, the first just ensures that the file is removed if it exists:\n",
    "\n",
    "!rm world_bank.json.gz -f <br>\n",
    "!wget https://raw.githubusercontent.com/bradenrc/sparksql_pot/master/world_bank.json.gz<br><br>\n",
    " <div class=\"panel-group\" id=\"accordion-2\">\n",
    "  <div class=\"panel panel-default\">\n",
    "    <div class=\"panel-heading\">\n",
    "      <h4 class=\"panel-title\">\n",
    "        <a data-toggle=\"collapse\" data-parent=\"#accordion-1\" href=\"#collapse1-2\">\n",
    "        Advanced Optional 1</a>\n",
    "      </h4>\n",
    "    </div>\n",
    "    <div id=\"collapse1-2\" class=\"panel-collapse collapse\">\n",
    "      <div class=\"panel-body\">Comment out the rm statement i.e. #!rm and re-run this section.   What is the name of the downloaded file?</div>\n",
    "    </div>\n",
    "  </div>\n",
    "  <div class=\"panel panel-default\">\n",
    "    <div class=\"panel-heading\">\n",
    "      <h4 class=\"panel-title\">\n",
    "        <a data-toggle=\"collapse\" data-parent=\"#accordion-2\" href=\"#collapse2-2\">\n",
    "        Advanced Optional 2</a>\n",
    "      </h4>\n",
    "    </div>\n",
    "    <div id=\"collapse2-2\" class=\"panel-collapse collapse\">\n",
    "      <div class=\"panel-body\">Add !ls to see all the files currently in storage.   Try running !mkdir testdir</div>\n",
    "    </div>\n",
    "  </div>\n",
    "  <div class=\"panel panel-default\">\n",
    "    <div class=\"panel-heading\">\n",
    "      <h4 class=\"panel-title\">\n",
    "        <a data-toggle=\"collapse\" data-parent=\"#accordion-2\" href=\"#collapse3-2\">\n",
    "        Advanced Optional 3</a>\n",
    "      </h4>\n",
    "    </div>\n",
    "    <div id=\"collapse3-2\" class=\"panel-collapse collapse\">\n",
    "      <div class=\"panel-body\">Clean up all added files/directories.   Use !rmdir to remove a directory.</div>\n",
    "    </div>\n",
    "  </div>\n",
    "</div> \n"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 2,
   "metadata": {
    "collapsed": false
   },
   "outputs": [
    {
     "name": "stdout",
     "output_type": "stream",
     "text": [
      "--2016-11-16 14:58:48--  https://raw.githubusercontent.com/bradenrc/sparksql_pot/master/world_bank.json.gz\n",
      "Resolving raw.githubusercontent.com (raw.githubusercontent.com)... 151.101.48.133\n",
      "Connecting to raw.githubusercontent.com (raw.githubusercontent.com)|151.101.48.133|:443... connected.\n",
      "HTTP request sent, awaiting response... 200 OK\n",
      "Length: 446287 (436K) [application/octet-stream]\n",
      "Saving to: 'world_bank.json.gz'\n",
      "\n",
      "100%[======================================>] 446,287     --.-K/s   in 0.02s   \n",
      "\n",
      "2016-11-16 14:58:48 (19.2 MB/s) - 'world_bank.json.gz' saved [446287/446287]\n",
      "\n"
     ]
    }
   ],
   "source": [
    "#Download file here\n",
    "!rm world_bank.json.gz* -f\n",
    "!wget https://raw.githubusercontent.com/bradenrc/sparksql_pot/master/world_bank.json.gz"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "## Step 3 - Create a Dataframe \n",
    "<br>\n",
    "Use the SparkSession you created earlier to read the World Bank json data - <i>world_bank.json.gz</i> as a Dataframe</a><br><br>\n",
    " <div class=\"panel-group\" id=\"accordion-3\">\n",
    "  <div class=\"panel panel-default\">\n",
    "    <div class=\"panel-heading\">\n",
    "      <h4 class=\"panel-title\">\n",
    "        <a data-toggle=\"collapse\" data-parent=\"#accordion-3\" href=\"#collapse1-3\">\n",
    "        Hint 1</a>\n",
    "      </h4>\n",
    "    </div>\n",
    "    <div id=\"collapse1-3\" class=\"panel-collapse collapse\">\n",
    "      <div class=\"panel-body\">Use the <i>read</i> function to return a Dataframe reader</div>\n",
    "    </div>\n",
    "  </div>\n",
    "  <div class=\"panel panel-default\">\n",
    "    <div class=\"panel-heading\">\n",
    "      <h4 class=\"panel-title\">\n",
    "        <a data-toggle=\"collapse\" data-parent=\"#accordion-3\" href=\"#collapse2-3\">\n",
    "        Hint 2</a>\n",
    "      </h4>\n",
    "    </div>\n",
    "    <div id=\"collapse2-3\" class=\"panel-collapse collapse\">\n",
    "      <div class=\"panel-body\">Use the <i>json()</i> method in Dataframe to read the file.   Note that the method handles a gzipped file format.</div>\n",
    "    </div>\n",
    "  </div>\n",
    "  <div class=\"panel panel-default\">\n",
    "    <div class=\"panel-heading\">\n",
    "      <h4 class=\"panel-title\">\n",
    "        <a data-toggle=\"collapse\" data-parent=\"#accordion-3\" href=\"#collapse3-3\">\n",
    "        Hint 3</a>\n",
    "      </h4>\n",
    "    </div>\n",
    "    <div id=\"collapse3-3\" class=\"panel-collapse collapse\">\n",
    "      <div class=\"panel-body\">To create the Dataframe type:<br>\n",
    "\n",
    "example1_df = spark.read.json(\"world_bank.json.gz\")<br></div>\n",
    "    </div>\n",
    "  </div>\n",
    "  <div class=\"panel panel-default\">\n",
    "    <div class=\"panel-heading\">\n",
    "      <h4 class=\"panel-title\">\n",
    "        <a data-toggle=\"collapse\" data-parent=\"#accordion-4\" href=\"#collapse4-3\">\n",
    "        Advanced Optional</a>\n",
    "      </h4>\n",
    "    </div>\n",
    "    <div id=\"collapse4-3\" class=\"panel-collapse collapse\">\n",
    "      <div class=\"panel-body\">Obtain the same result by using <i>textFile()</i> to read the file as RDD and then convert to a Dataframe</div>\n",
    "    </div>\n",
    "  </div>\n",
    "</div> \n"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 3,
   "metadata": {
    "collapsed": false
   },
   "outputs": [],
   "source": [
    "#Create the Dataframe here:\n",
    "example1_df = spark.read.json(\"world_bank.json.gz\")\n",
    "\n",
    "#Advanced Solution\n",
    "#example1_rdd = sc.textFile(\"world_bank.json.gz\")\n",
    "#example1_df = spark.read.json(example1_rdd)"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    " ## Step 3.1 - Show the Dataframe schema\n",
    " <br>\n",
    " <div class=\"panel-group\" id=\"accordion-31\">\n",
    "  <div class=\"panel panel-default\">\n",
    "    <div class=\"panel-heading\">\n",
    "      <h4 class=\"panel-title\">\n",
    "        <a data-toggle=\"collapse\" data-parent=\"#accordion-1\" href=\"#collapse1-31\">\n",
    "        Hint 1</a>\n",
    "      </h4>\n",
    "    </div>\n",
    "    <div id=\"collapse1-31\" class=\"panel-collapse collapse\">\n",
    "      <div class=\"panel-body\"><h3>We can look at the schema with this command:</h3>\n",
    "\n",
    "Type: <br>\n",
    "example1_df.printSchema()</div>\n",
    "    </div>\n",
    "  </div>\n",
    "  <div class=\"panel panel-default\">\n",
    "    <div class=\"panel-heading\">\n",
    "      <h4 class=\"panel-title\">\n",
    "        <a data-toggle=\"collapse\" data-parent=\"#accordion-31\" href=\"#collapse2-31\">\n",
    "        Advanced Optional 1</a>\n",
    "      </h4>\n",
    "    </div>\n",
    "    <div id=\"collapse2-31\" class=\"panel-collapse collapse\">\n",
    "      <div class=\"panel-body\">Get the dataframe columns.   Try using command-completion (use TAB after the .) to obtain the list of possible methods/values</div>\n",
    "    </div>\n",
    "  </div>\n",
    "  <div class=\"panel panel-default\">\n",
    "    <div class=\"panel-heading\">\n",
    "      <h4 class=\"panel-title\">\n",
    "        <a data-toggle=\"collapse\" data-parent=\"#accordion-31\" href=\"#collapse3-31\">\n",
    "        Advanced Optional 2</a>\n",
    "      </h4>\n",
    "    </div>\n",
    "    <div id=\"collapse3-31\" class=\"panel-collapse collapse\">\n",
    "      <div class=\"panel-body\">Convert the dataframe back to JSON and print the first value</div>\n",
    "    </div>\n",
    "  </div>\n",
    "</div>"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 4,
   "metadata": {
    "collapsed": false
   },
   "outputs": [
    {
     "name": "stdout",
     "output_type": "stream",
     "text": [
      "root\n",
      " |-- _id: struct (nullable = true)\n",
      " |    |-- $oid: string (nullable = true)\n",
      " |-- approvalfy: string (nullable = true)\n",
      " |-- board_approval_month: string (nullable = true)\n",
      " |-- boardapprovaldate: string (nullable = true)\n",
      " |-- borrower: string (nullable = true)\n",
      " |-- closingdate: string (nullable = true)\n",
      " |-- country_namecode: string (nullable = true)\n",
      " |-- countrycode: string (nullable = true)\n",
      " |-- countryname: string (nullable = true)\n",
      " |-- countryshortname: string (nullable = true)\n",
      " |-- docty: string (nullable = true)\n",
      " |-- envassesmentcategorycode: string (nullable = true)\n",
      " |-- grantamt: long (nullable = true)\n",
      " |-- ibrdcommamt: long (nullable = true)\n",
      " |-- id: string (nullable = true)\n",
      " |-- idacommamt: long (nullable = true)\n",
      " |-- impagency: string (nullable = true)\n",
      " |-- lendinginstr: string (nullable = true)\n",
      " |-- lendinginstrtype: string (nullable = true)\n",
      " |-- lendprojectcost: long (nullable = true)\n",
      " |-- majorsector_percent: array (nullable = true)\n",
      " |    |-- element: struct (containsNull = true)\n",
      " |    |    |-- Name: string (nullable = true)\n",
      " |    |    |-- Percent: long (nullable = true)\n",
      " |-- mjsector_namecode: array (nullable = true)\n",
      " |    |-- element: struct (containsNull = true)\n",
      " |    |    |-- code: string (nullable = true)\n",
      " |    |    |-- name: string (nullable = true)\n",
      " |-- mjtheme: array (nullable = true)\n",
      " |    |-- element: string (containsNull = true)\n",
      " |-- mjtheme_namecode: array (nullable = true)\n",
      " |    |-- element: struct (containsNull = true)\n",
      " |    |    |-- code: string (nullable = true)\n",
      " |    |    |-- name: string (nullable = true)\n",
      " |-- mjthemecode: string (nullable = true)\n",
      " |-- prodline: string (nullable = true)\n",
      " |-- prodlinetext: string (nullable = true)\n",
      " |-- productlinetype: string (nullable = true)\n",
      " |-- project_abstract: struct (nullable = true)\n",
      " |    |-- cdata: string (nullable = true)\n",
      " |-- project_name: string (nullable = true)\n",
      " |-- projectdocs: array (nullable = true)\n",
      " |    |-- element: struct (containsNull = true)\n",
      " |    |    |-- DocDate: string (nullable = true)\n",
      " |    |    |-- DocType: string (nullable = true)\n",
      " |    |    |-- DocTypeDesc: string (nullable = true)\n",
      " |    |    |-- DocURL: string (nullable = true)\n",
      " |    |    |-- EntityID: string (nullable = true)\n",
      " |-- projectfinancialtype: string (nullable = true)\n",
      " |-- projectstatusdisplay: string (nullable = true)\n",
      " |-- regionname: string (nullable = true)\n",
      " |-- sector: array (nullable = true)\n",
      " |    |-- element: struct (containsNull = true)\n",
      " |    |    |-- Name: string (nullable = true)\n",
      " |-- sector1: struct (nullable = true)\n",
      " |    |-- Name: string (nullable = true)\n",
      " |    |-- Percent: long (nullable = true)\n",
      " |-- sector2: struct (nullable = true)\n",
      " |    |-- Name: string (nullable = true)\n",
      " |    |-- Percent: long (nullable = true)\n",
      " |-- sector3: struct (nullable = true)\n",
      " |    |-- Name: string (nullable = true)\n",
      " |    |-- Percent: long (nullable = true)\n",
      " |-- sector4: struct (nullable = true)\n",
      " |    |-- Name: string (nullable = true)\n",
      " |    |-- Percent: long (nullable = true)\n",
      " |-- sector_namecode: array (nullable = true)\n",
      " |    |-- element: struct (containsNull = true)\n",
      " |    |    |-- code: string (nullable = true)\n",
      " |    |    |-- name: string (nullable = true)\n",
      " |-- sectorcode: string (nullable = true)\n",
      " |-- source: string (nullable = true)\n",
      " |-- status: string (nullable = true)\n",
      " |-- supplementprojectflg: string (nullable = true)\n",
      " |-- theme1: struct (nullable = true)\n",
      " |    |-- Name: string (nullable = true)\n",
      " |    |-- Percent: long (nullable = true)\n",
      " |-- theme_namecode: array (nullable = true)\n",
      " |    |-- element: struct (containsNull = true)\n",
      " |    |    |-- code: string (nullable = true)\n",
      " |    |    |-- name: string (nullable = true)\n",
      " |-- themecode: string (nullable = true)\n",
      " |-- totalamt: long (nullable = true)\n",
      " |-- totalcommamt: long (nullable = true)\n",
      " |-- url: string (nullable = true)\n",
      "\n"
     ]
    }
   ],
   "source": [
    "#Print out the schema\n",
    "example1_df.printSchema()\n",
    "\n",
    "#Advanced Option 1\n",
    "#example1_df.columns\n",
    "\n",
    "#Advanced Option 2\n",
    "#example1_df.toJSON().first()"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "## Step 3.2 - Using the Dataframe\n",
    "<br>\n",
    "Dataframes are a subset of RDDs and can be similarly transformed.  You can map and filter them.\n",
    "<br>Take a look at the first two rows of data using the [take()](http://spark.apache.org/docs/latest/api/python/pyspark.sql.html?highlight=take#pyspark.sql.DataFrame.take) function.<br>\n",
    "<div class=\"panel-group\" id=\"accordion-1\">\n",
    "  <div class=\"panel panel-default\">\n",
    "    <div class=\"panel-heading\">\n",
    "      <h4 class=\"panel-title\">\n",
    "        <a data-toggle=\"collapse\" data-parent=\"#accordion-32\" href=\"#collapse1-32\">\n",
    "        Hint 1</a>\n",
    "      </h4>\n",
    "    </div>\n",
    "    <div id=\"collapse1-32\" class=\"panel-collapse collapse\">\n",
    "      <div class=\"panel-body\">example1_df.take(2)</div>\n",
    "    </div>\n",
    "  </div>\n",
    "  <div class=\"panel panel-default\">\n",
    "    <div class=\"panel-heading\">\n",
    "      <h4 class=\"panel-title\">\n",
    "        <a data-toggle=\"collapse\" data-parent=\"#accordion-32\" href=\"#collapse2-32\">\n",
    "        Advanced Optional 1</a>\n",
    "      </h4>\n",
    "    </div>\n",
    "    <div id=\"collapse2-32\" class=\"panel-collapse collapse\">\n",
    "      <div class=\"panel-body\"><i>take()</i> returns data as an RDD list of Row objects.   <i>show()</i> prints the objects to the console.   What is the default number of rows displayed?</div>\n",
    "    </div>\n",
    "  </div>\n",
    "  <div class=\"panel panel-default\">\n",
    "    <div class=\"panel-heading\">\n",
    "      <h4 class=\"panel-title\">\n",
    "        <a data-toggle=\"collapse\" data-parent=\"#accordion-32\" href=\"#collapse3-32\">\n",
    "        Advanced Optional 2</a>\n",
    "      </h4>\n",
    "    </div>\n",
    "    <div id=\"collapse3-32\" class=\"panel-collapse collapse\">\n",
    "      <div class=\"panel-body\">Save the table as a parquet table.   Use !ls to confirm it was saved.  Use a <i><a href=\"https://spark.apache.org/docs/1.6.2/api/python/pyspark.sql.html#pyspark.sql.DataFrameWriter\"DataFrameWriter></a></i>  What did you see when you ran the ls command?</div>\n",
    "    </div>\n",
    "  </div>\n",
    "</div> \n",
    " \n",
    "\n"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 5,
   "metadata": {
    "collapsed": false
   },
   "outputs": [
    {
     "data": {
      "text/plain": [
       "[Row(_id=Row($oid=u'52b213b38594d8a2be17c780'), approvalfy=u'1999', board_approval_month=u'November', boardapprovaldate=u'2013-11-12T00:00:00Z', borrower=u'FEDERAL DEMOCRATIC REPUBLIC OF ETHIOPIA', closingdate=u'2018-07-07T00:00:00Z', country_namecode=u'Federal Democratic Republic of Ethiopia!$!ET', countrycode=u'ET', countryname=u'Federal Democratic Republic of Ethiopia', countryshortname=u'Ethiopia', docty=u'Project Information Document,Indigenous Peoples Plan,Project Information Document', envassesmentcategorycode=u'C', grantamt=0, ibrdcommamt=0, id=u'P129828', idacommamt=130000000, impagency=u'MINISTRY OF EDUCATION', lendinginstr=u'Investment Project Financing', lendinginstrtype=u'IN', lendprojectcost=550000000, majorsector_percent=[Row(Name=u'Education', Percent=46), Row(Name=u'Education', Percent=26), Row(Name=u'Public Administration, Law, and Justice', Percent=16), Row(Name=u'Education', Percent=12)], mjsector_namecode=[Row(code=u'EX', name=u'Education'), Row(code=u'EX', name=u'Education'), Row(code=u'BX', name=u'Public Administration, Law, and Justice'), Row(code=u'EX', name=u'Education')], mjtheme=[u'Human development'], mjtheme_namecode=[Row(code=u'8', name=u'Human development'), Row(code=u'11', name=u'')], mjthemecode=u'8,11', prodline=u'PE', prodlinetext=u'IBRD/IDA', productlinetype=u'L', project_abstract=Row(cdata=u'The development objective of the Second Phase of General Education Quality Improvement Project for Ethiopia is to improve learning conditions in primary and secondary schools and strengthen institutions at different levels of educational administration. The project has six components. The first component is curriculum, textbooks, assessment, examinations, and inspection. This component will support improvement of learning conditions in grades KG-12 by providing increased access to teaching and learning materials and through improvements to the curriculum by assessing the strengths and weaknesses of the current curriculum. This component has following four sub-components: (i) curriculum reform and implementation; (ii) teaching and learning materials; (iii) assessment and examinations; and (iv) inspection. The second component is teacher development program (TDP). This component will support improvements in learning conditions in both primary and secondary schools by advancing the quality of teaching in general education through: (a) enhancing the training of pre-service teachers in teacher education institutions; and (b) improving the quality of in-service teacher training. This component has following three sub-components: (i) pre-service teacher training; (ii) in-service teacher training; and (iii) licensing and relicensing of teachers and school leaders. The third component is school improvement plan. This component will support the strengthening of school planning in order to improve learning outcomes, and to partly fund the school improvement plans through school grants. It has following two sub-components: (i) school improvement plan; and (ii) school grants. The fourth component is management and capacity building, including education management information systems (EMIS). This component will support management and capacity building aspect of the project. This component has following three sub-components: (i) capacity building for education planning and management; (ii) capacity building for school planning and management; and (iii) EMIS. The fifth component is improving the quality of learning and teaching in secondary schools and universities through the use of information and communications technology (ICT). It has following five sub-components: (i) national policy and institution for ICT in general education; (ii) national ICT infrastructure improvement plan for general education; (iii) develop an integrated monitoring, evaluation, and learning system specifically for the ICT component; (iv) teacher professional development in the use of ICT; and (v) provision of limited number of e-Braille display readers with the possibility to scale up to all secondary education schools based on the successful implementation and usage of the readers. The sixth component is program coordination, monitoring and evaluation, and communication. It will support institutional strengthening by developing capacities in all aspects of program coordination, monitoring and evaluation; a new sub-component on communications will support information sharing for better management and accountability. It has following three sub-components: (i) program coordination; (ii) monitoring and evaluation (M and E); and (iii) communication.'), project_name=u'Ethiopia General Education Quality Improvement Project II', projectdocs=[Row(DocDate=u'28-AUG-2013', DocType=u'PID', DocTypeDesc=u'Project Information Document (PID),  Vol.', DocURL=u'http://www-wds.worldbank.org/servlet/WDSServlet?pcont=details&eid=090224b081e545fb_1_0', EntityID=u'090224b081e545fb_1_0'), Row(DocDate=u'01-JUL-2013', DocType=u'IP', DocTypeDesc=u'Indigenous Peoples Plan (IP),  Vol.1 of 1', DocURL=u'http://www-wds.worldbank.org/servlet/WDSServlet?pcont=details&eid=000442464_20130920111729', EntityID=u'000442464_20130920111729'), Row(DocDate=u'22-NOV-2012', DocType=u'PID', DocTypeDesc=u'Project Information Document (PID),  Vol.', DocURL=u'http://www-wds.worldbank.org/servlet/WDSServlet?pcont=details&eid=090224b0817b19e2_1_0', EntityID=u'090224b0817b19e2_1_0')], projectfinancialtype=u'IDA', projectstatusdisplay=u'Active', regionname=u'Africa', sector=[Row(Name=u'Primary education'), Row(Name=u'Secondary education'), Row(Name=u'Public administration- Other social services'), Row(Name=u'Tertiary education')], sector1=Row(Name=u'Primary education', Percent=46), sector2=Row(Name=u'Secondary education', Percent=26), sector3=Row(Name=u'Public administration- Other social services', Percent=16), sector4=Row(Name=u'Tertiary education', Percent=12), sector_namecode=[Row(code=u'EP', name=u'Primary education'), Row(code=u'ES', name=u'Secondary education'), Row(code=u'BS', name=u'Public administration- Other social services'), Row(code=u'ET', name=u'Tertiary education')], sectorcode=u'ET,BS,ES,EP', source=u'IBRD', status=u'Active', supplementprojectflg=u'N', theme1=Row(Name=u'Education for all', Percent=100), theme_namecode=[Row(code=u'65', name=u'Education for all')], themecode=u'65', totalamt=130000000, totalcommamt=130000000, url=u'http://www.worldbank.org/projects/P129828/ethiopia-general-education-quality-improvement-project-ii?lang=en'),\n",
       " Row(_id=Row($oid=u'52b213b38594d8a2be17c781'), approvalfy=u'2015', board_approval_month=u'November', boardapprovaldate=u'2013-11-04T00:00:00Z', borrower=u'GOVERNMENT OF TUNISIA', closingdate=None, country_namecode=u'Republic of Tunisia!$!TN', countrycode=u'TN', countryname=u'Republic of Tunisia', countryshortname=u'Tunisia', docty=u'Project Information Document,Integrated Safeguards Data Sheet,Integrated Safeguards Data Sheet,Project Information Document,Integrated Safeguards Data Sheet,Project Information Document', envassesmentcategorycode=u'C', grantamt=4700000, ibrdcommamt=0, id=u'P144674', idacommamt=0, impagency=u'MINISTRY OF FINANCE', lendinginstr=u'Specific Investment Loan', lendinginstrtype=u'IN', lendprojectcost=5700000, majorsector_percent=[Row(Name=u'Public Administration, Law, and Justice', Percent=70), Row(Name=u'Public Administration, Law, and Justice', Percent=30)], mjsector_namecode=[Row(code=u'BX', name=u'Public Administration, Law, and Justice'), Row(code=u'BX', name=u'Public Administration, Law, and Justice')], mjtheme=[u'Economic management', u'Social protection and risk management'], mjtheme_namecode=[Row(code=u'1', name=u'Economic management'), Row(code=u'6', name=u'Social protection and risk management')], mjthemecode=u'1,6', prodline=u'RE', prodlinetext=u'Recipient Executed Activities', productlinetype=u'L', project_abstract=None, project_name=u'TN: DTF Social Protection Reforms Support', projectdocs=[Row(DocDate=u'29-MAR-2013', DocType=u'PID', DocTypeDesc=u'Project Information Document (PID),  Vol.1 of 1', DocURL=u'http://www-wds.worldbank.org/servlet/WDSServlet?pcont=details&eid=000333037_20131024115616', EntityID=u'000333037_20131024115616'), Row(DocDate=u'29-MAR-2013', DocType=u'ISDS', DocTypeDesc=u'Integrated Safeguards Data Sheet (ISDS),  Vol.1 of 1', DocURL=u'http://www-wds.worldbank.org/servlet/WDSServlet?pcont=details&eid=000356161_20131024151611', EntityID=u'000356161_20131024151611'), Row(DocDate=u'29-MAR-2013', DocType=u'ISDS', DocTypeDesc=u'Integrated Safeguards Data Sheet (ISDS),  Vol.1 of 1', DocURL=u'http://www-wds.worldbank.org/servlet/WDSServlet?pcont=details&eid=000442464_20131031112136', EntityID=u'000442464_20131031112136'), Row(DocDate=u'29-MAR-2013', DocType=u'PID', DocTypeDesc=u'Project Information Document (PID),  Vol.1 of 1', DocURL=u'http://www-wds.worldbank.org/servlet/WDSServlet?pcont=details&eid=000333037_20131031105716', EntityID=u'000333037_20131031105716'), Row(DocDate=u'16-JAN-2013', DocType=u'ISDS', DocTypeDesc=u'Integrated Safeguards Data Sheet (ISDS),  Vol.1 of 1', DocURL=u'http://www-wds.worldbank.org/servlet/WDSServlet?pcont=details&eid=000356161_20130305113209', EntityID=u'000356161_20130305113209'), Row(DocDate=u'16-JAN-2013', DocType=u'PID', DocTypeDesc=u'Project Information Document (PID),  Vol.1 of 1', DocURL=u'http://www-wds.worldbank.org/servlet/WDSServlet?pcont=details&eid=000356161_20130305113716', EntityID=u'000356161_20130305113716')], projectfinancialtype=u'OTHER', projectstatusdisplay=u'Active', regionname=u'Middle East and North Africa', sector=[Row(Name=u'Public administration- Other social services'), Row(Name=u'General public administration sector')], sector1=Row(Name=u'Public administration- Other social services', Percent=70), sector2=Row(Name=u'General public administration sector', Percent=30), sector3=None, sector4=None, sector_namecode=[Row(code=u'BS', name=u'Public administration- Other social services'), Row(code=u'BZ', name=u'General public administration sector')], sectorcode=u'BZ,BS', source=u'IBRD', status=u'Active', supplementprojectflg=u'N', theme1=Row(Name=u'Other economic management', Percent=30), theme_namecode=[Row(code=u'24', name=u'Other economic management'), Row(code=u'54', name=u'Social safety nets')], themecode=u'54,24', totalamt=0, totalcommamt=4700000, url=u'http://www.worldbank.org/projects/P144674?lang=en')]"
      ]
     },
     "execution_count": 5,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "#Use take on the DataFrame to pull out 2 rows\n",
    "example1_df.take(2)\n",
    "\n",
    "#Advanced Option 1\n",
    "#example1_df.show()\n",
    "\n",
    "#Advanced Option 2\n",
    "#example1_df.write.parquet('parquet_file')\n",
    "#!ls -l parquet_file"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "## Step 4 - Register a Temp Table\n",
    "<br>\n",
    "SQL works on tables.   Currently we have data in a dataframe, but we have no table identifier for it.   Thus, we want to create a temporary table reference that refers to this dataframe.\n",
    "<br>\n",
    "<div class=\"panel-group\" id=\"accordion-4\">\n",
    "  <div class=\"panel panel-default\">\n",
    "    <div class=\"panel-heading\">\n",
    "      <h4 class=\"panel-title\">\n",
    "        <a data-toggle=\"collapse\" data-parent=\"#accordion-4\" href=\"#collapse1-4\">\n",
    "        Hint 1</a>\n",
    "      </h4>\n",
    "    </div>\n",
    "    <div id=\"collapse1-4\" class=\"panel-collapse collapse\">\n",
    "      <div class=\"panel-body\">The function is: DataframeObject.createTempView(\"name_of_table\")<br>\n",
    "Create a table named \"world_bank\"<br></div>\n",
    "    </div>\n",
    "  </div>\n",
    "  <div class=\"panel panel-default\">\n",
    "    <div class=\"panel-heading\">\n",
    "      <h4 class=\"panel-title\">\n",
    "        <a data-toggle=\"collapse\" data-parent=\"#accordion-4\" href=\"#collapse2-4\">\n",
    "        Hint 2</a>\n",
    "      </h4>\n",
    "    </div>\n",
    "    <div id=\"collapse2-4\" class=\"panel-collapse collapse\">\n",
    "      <div class=\"panel-body\">example1_df.(\"world_bank\")</div>\n",
    "    </div>\n",
    "  </div>\n",
    "  <div class=\"panel panel-default\">\n",
    "    <div class=\"panel-heading\">\n",
    "      <h4 class=\"panel-title\">\n",
    "        <a data-toggle=\"collapse\" data-parent=\"#accordion-4\" href=\"#collapse3-4\">\n",
    "        Advanced Optional 1</a>\n",
    "      </h4>\n",
    "    </div>\n",
    "    <div id=\"collapse3-4\" class=\"panel-collapse collapse\">\n",
    "      <div class=\"panel-body\">You'll need to create a [catalog](http://spark.apache.org/docs/latest/api/python/pyspark.sql.html?highlight=catalog#pyspark.sql.SparkSession.catalog) object</div>\n",
    "    </div>\n",
    "  </div>\n",
    "  <div class=\"panel panel-default\">\n",
    "    <div class=\"panel-heading\">\n",
    "      <h4 class=\"panel-title\">\n",
    "        <a data-toggle=\"collapse\" data-parent=\"#accordion-4\" href=\"#collapse4-4\">\n",
    "        Advanced Optional 2</a>\n",
    "      </h4>\n",
    "    </div>\n",
    "    <div id=\"collapse4-4\" class=\"panel-collapse collapse\">\n",
    "      <div class=\"panel-body\">Try creating a second temporary table on the same dataframe.   What does <i>listTables()</i> return?</div>\n",
    "    </div>\n",
    "  </div>\n",
    "    <div class=\"panel panel-default\">\n",
    "    <div class=\"panel-heading\">\n",
    "      <h4 class=\"panel-title\">\n",
    "        <a data-toggle=\"collapse\" data-parent=\"#accordion-4\" href=\"#collapse5-4\">\n",
    "        Advanced Optional 3</a>\n",
    "      </h4>\n",
    "    </div>\n",
    "    <div id=\"collapse5-4\" class=\"panel-collapse collapse\">\n",
    "      <div class=\"panel-body\">Drop the additional temp table.   What does <i>listTables()</i> return?</div>\n",
    "    </div>\n",
    "  </div>\n",
    "</div>\n",
    "\n"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 6,
   "metadata": {
    "collapsed": false,
    "scrolled": false
   },
   "outputs": [],
   "source": [
    "#Create the table to be referenced via SparkSQL\n",
    "example1_df.createTempView(\"world_bank\")\n",
    "\n",
    "#Advanced Optional 1\n",
    "#catalog = spark.catalog\n",
    "#print catalog.listTables()\n",
    "\n",
    "#Advanced Optional 2\n",
    "#example1_df.createTempView(\"world_bank1\")\n",
    "\n",
    "#Advanced Optional 2\n",
    "#catalog.dropTempView(\"world_bank1\");\n",
    "#catalog.listTables()"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "## Step 5 - Writing SQL Statements\n",
    "<br>\n",
    "Write SQL statements to return two rows from the world_bank table.\n",
    "<br>\n",
    " <div class=\"panel-group\" id=\"accordion-5\">\n",
    "  <div class=\"panel panel-default\">\n",
    "    <div class=\"panel-heading\">\n",
    "      <h4 class=\"panel-title\">\n",
    "        <a data-toggle=\"collapse\" data-parent=\"#accordion-5\" href=\"#collapse1-5\">\n",
    "        Hint 1</a>\n",
    "      </h4>\n",
    "    </div>\n",
    "    <div id=\"collapse1-5\" class=\"panel-collapse collapse\">\n",
    "      <div class=\"panel-body\">Use the <i>sql()</i> method on your SparkSession</div>\n",
    "    </div>\n",
    "  </div>\n",
    "  <div class=\"panel panel-default\">\n",
    "    <div class=\"panel-heading\">\n",
    "      <h4 class=\"panel-title\">\n",
    "        <a data-toggle=\"collapse\" data-parent=\"#accordion-5\" href=\"#collapse2-5\">\n",
    "        Hint 2</a>\n",
    "      </h4>\n",
    "    </div>\n",
    "    <div id=\"collapse2-5\" class=\"panel-collapse collapse\">\n",
    "      <div class=\"panel-body\">Use <i>limit</i> (i.e. <i>limit 2</i>) within your SQL statement to limit the number of rows returned.   Use <i>show()</i> to display the values.</div>\n",
    "    </div>\n",
    "  </div>\n",
    "  <div class=\"panel panel-default\">\n",
    "    <div class=\"panel-heading\">\n",
    "      <h4 class=\"panel-title\">\n",
    "        <a data-toggle=\"collapse\" data-parent=\"#accordion-5\" href=\"#collapse3-5\">\n",
    "        Hint 3</a>\n",
    "      </h4>\n",
    "    </div>\n",
    "    <div id=\"collapse3-5\" class=\"panel-collapse collapse\">\n",
    "      <div class=\"panel-body\">Type:<br>\n",
    "      spark.sql(\"select * from world_bank limit 2\").show()<br></div>\n",
    "    </div>\n",
    "  </div>\n",
    "</div> \n"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 7,
   "metadata": {
    "collapsed": false
   },
   "outputs": [
    {
     "name": "stdout",
     "output_type": "stream",
     "text": [
      "+--------------------+----------+--------------------+--------------------+--------------------+--------------------+--------------------+-----------+--------------------+----------------+--------------------+------------------------+--------+-----------+-------+----------+--------------------+--------------------+----------------+---------------+--------------------+--------------------+--------------------+--------------------+-----------+--------+--------------------+---------------+--------------------+--------------------+--------------------+--------------------+--------------------+--------------------+--------------------+--------------------+--------------------+--------------------+--------------------+--------------------+-----------+------+------+--------------------+--------------------+--------------------+---------+---------+------------+--------------------+\n",
      "|                 _id|approvalfy|board_approval_month|   boardapprovaldate|            borrower|         closingdate|    country_namecode|countrycode|         countryname|countryshortname|               docty|envassesmentcategorycode|grantamt|ibrdcommamt|     id|idacommamt|           impagency|        lendinginstr|lendinginstrtype|lendprojectcost| majorsector_percent|   mjsector_namecode|             mjtheme|    mjtheme_namecode|mjthemecode|prodline|        prodlinetext|productlinetype|    project_abstract|        project_name|         projectdocs|projectfinancialtype|projectstatusdisplay|          regionname|              sector|             sector1|             sector2|             sector3|             sector4|     sector_namecode| sectorcode|source|status|supplementprojectflg|              theme1|      theme_namecode|themecode| totalamt|totalcommamt|                 url|\n",
      "+--------------------+----------+--------------------+--------------------+--------------------+--------------------+--------------------+-----------+--------------------+----------------+--------------------+------------------------+--------+-----------+-------+----------+--------------------+--------------------+----------------+---------------+--------------------+--------------------+--------------------+--------------------+-----------+--------+--------------------+---------------+--------------------+--------------------+--------------------+--------------------+--------------------+--------------------+--------------------+--------------------+--------------------+--------------------+--------------------+--------------------+-----------+------+------+--------------------+--------------------+--------------------+---------+---------+------------+--------------------+\n",
      "|[52b213b38594d8a2...|      1999|            November|2013-11-12T00:00:00Z|FEDERAL DEMOCRATI...|2018-07-07T00:00:00Z|Federal Democrati...|         ET|Federal Democrati...|        Ethiopia|Project Informati...|                       C|       0|          0|P129828| 130000000|MINISTRY OF EDUCA...|Investment Projec...|              IN|      550000000|[[Education,46], ...|[[EX,Education], ...| [Human development]|[[8,Human develop...|       8,11|      PE|            IBRD/IDA|              L|[The development ...|Ethiopia General ...|[[28-AUG-2013,PID...|                 IDA|              Active|              Africa|[[Primary educati...|[Primary educatio...|[Secondary educat...|[Public administr...|[Tertiary educati...|[[EP,Primary educ...|ET,BS,ES,EP|  IBRD|Active|                   N|[Education for al...|[[65,Education fo...|       65|130000000|   130000000|http://www.worldb...|\n",
      "|[52b213b38594d8a2...|      2015|            November|2013-11-04T00:00:00Z|GOVERNMENT OF TUN...|                null|Republic of Tunis...|         TN| Republic of Tunisia|         Tunisia|Project Informati...|                       C| 4700000|          0|P144674|         0| MINISTRY OF FINANCE|Specific Investme...|              IN|        5700000|[[Public Administ...|[[BX,Public Admin...|[Economic managem...|[[1,Economic mana...|        1,6|      RE|Recipient Execute...|              L|                null|TN: DTF Social Pr...|[[29-MAR-2013,PID...|               OTHER|              Active|Middle East and N...|[[Public administ...|[Public administr...|[General public a...|                null|                null|[[BS,Public admin...|      BZ,BS|  IBRD|Active|                   N|[Other economic m...|[[24,Other econom...|    54,24|        0|     4700000|http://www.worldb...|\n",
      "+--------------------+----------+--------------------+--------------------+--------------------+--------------------+--------------------+-----------+--------------------+----------------+--------------------+------------------------+--------+-----------+-------+----------+--------------------+--------------------+----------------+---------------+--------------------+--------------------+--------------------+--------------------+-----------+--------+--------------------+---------------+--------------------+--------------------+--------------------+--------------------+--------------------+--------------------+--------------------+--------------------+--------------------+--------------------+--------------------+--------------------+-----------+------+------+--------------------+--------------------+--------------------+---------+---------+------------+--------------------+\n",
      "\n"
     ]
    }
   ],
   "source": [
    "#Use SQL to query the table and print the output\n",
    "spark.sql(\"select * from world_bank limit 2\").show()"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "### Step 5.1 - Writing SQL Statements\n",
    "<br>\n",
    "Try writing the next three sections yourself first.   Each hint contains the solution for that section.   We provide this here because this is more SQL than Spark and not everyone is familar with SQL.  Nor is this an SQL class!\n",
    "<br><br>\n",
    " <div class=\"panel-group\" id=\"accordion-51\">\n",
    "  <div class=\"panel panel-default\">\n",
    "    <div class=\"panel-heading\">\n",
    "      <h4 class=\"panel-title\">\n",
    "        <a data-toggle=\"collapse\" data-parent=\"#accordion-51\" href=\"#collapse1-51\">\n",
    "        Hint 1</a>\n",
    "      </h4>\n",
    "    </div>\n",
    "    <div id=\"collapse1-51\" class=\"panel-collapse collapse\">\n",
    "      <div class=\"panel-body\">spark.sql(\"select * from world_bank limit 2\").toPandas()</div>\n",
    "    </div>\n",
    "  </div>\n",
    "  <div class=\"panel panel-default\">\n",
    "    <div class=\"panel-heading\">\n",
    "      <h4 class=\"panel-title\">\n",
    "        <a data-toggle=\"collapse\" data-parent=\"#accordion-51\" href=\"#collapse2-51\">\n",
    "        Hint 2</a>\n",
    "      </h4>\n",
    "    </div>\n",
    "    <div id=\"collapse2-51\" class=\"panel-collapse collapse\">\n",
    "      <div class=\"panel-body\">spark.sql(\"select regionname, count(*) as regioncount from world_bank group by regionname order by regioncount desc\").toPandas()</div>\n",
    "    </div>\n",
    "  </div>\n",
    "  <div class=\"panel panel-default\">\n",
    "    <div class=\"panel-heading\">\n",
    "      <h4 class=\"panel-title\">\n",
    "        <a data-toggle=\"collapse\" data-parent=\"#accordion-51\" href=\"#collapse3-51\">\n",
    "        Hint 3</a>\n",
    "      </h4>\n",
    "    </div>\n",
    "    <div id=\"collapse3-51\" class=\"panel-collapse collapse\">\n",
    "      <div class=\"panel-body\">spark.sql(\"select sector.Name from world_bank limit 5\").toPandas()</div>\n",
    "    </div>\n",
    "  </div>\n",
    "</div> "
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 8,
   "metadata": {
    "collapsed": false
   },
   "outputs": [
    {
     "data": {
      "text/html": [
       "<div>\n",
       "<table border=\"1\" class=\"dataframe\">\n",
       "  <thead>\n",
       "    <tr style=\"text-align: right;\">\n",
       "      <th></th>\n",
       "      <th>_id</th>\n",
       "      <th>approvalfy</th>\n",
       "      <th>board_approval_month</th>\n",
       "      <th>boardapprovaldate</th>\n",
       "      <th>borrower</th>\n",
       "      <th>closingdate</th>\n",
       "      <th>country_namecode</th>\n",
       "      <th>countrycode</th>\n",
       "      <th>countryname</th>\n",
       "      <th>countryshortname</th>\n",
       "      <th>...</th>\n",
       "      <th>sectorcode</th>\n",
       "      <th>source</th>\n",
       "      <th>status</th>\n",
       "      <th>supplementprojectflg</th>\n",
       "      <th>theme1</th>\n",
       "      <th>theme_namecode</th>\n",
       "      <th>themecode</th>\n",
       "      <th>totalamt</th>\n",
       "      <th>totalcommamt</th>\n",
       "      <th>url</th>\n",
       "    </tr>\n",
       "  </thead>\n",
       "  <tbody>\n",
       "    <tr>\n",
       "      <th>0</th>\n",
       "      <td>(52b213b38594d8a2be17c780,)</td>\n",
       "      <td>1999</td>\n",
       "      <td>November</td>\n",
       "      <td>2013-11-12T00:00:00Z</td>\n",
       "      <td>FEDERAL DEMOCRATIC REPUBLIC OF ETHIOPIA</td>\n",
       "      <td>2018-07-07T00:00:00Z</td>\n",
       "      <td>Federal Democratic Republic of Ethiopia!$!ET</td>\n",
       "      <td>ET</td>\n",
       "      <td>Federal Democratic Republic of Ethiopia</td>\n",
       "      <td>Ethiopia</td>\n",
       "      <td>...</td>\n",
       "      <td>ET,BS,ES,EP</td>\n",
       "      <td>IBRD</td>\n",
       "      <td>Active</td>\n",
       "      <td>N</td>\n",
       "      <td>(Education for all, 100)</td>\n",
       "      <td>[(65, Education for all)]</td>\n",
       "      <td>65</td>\n",
       "      <td>130000000</td>\n",
       "      <td>130000000</td>\n",
       "      <td>http://www.worldbank.org/projects/P129828/ethi...</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>1</th>\n",
       "      <td>(52b213b38594d8a2be17c781,)</td>\n",
       "      <td>2015</td>\n",
       "      <td>November</td>\n",
       "      <td>2013-11-04T00:00:00Z</td>\n",
       "      <td>GOVERNMENT OF TUNISIA</td>\n",
       "      <td>None</td>\n",
       "      <td>Republic of Tunisia!$!TN</td>\n",
       "      <td>TN</td>\n",
       "      <td>Republic of Tunisia</td>\n",
       "      <td>Tunisia</td>\n",
       "      <td>...</td>\n",
       "      <td>BZ,BS</td>\n",
       "      <td>IBRD</td>\n",
       "      <td>Active</td>\n",
       "      <td>N</td>\n",
       "      <td>(Other economic management, 30)</td>\n",
       "      <td>[(24, Other economic management), (54, Social ...</td>\n",
       "      <td>54,24</td>\n",
       "      <td>0</td>\n",
       "      <td>4700000</td>\n",
       "      <td>http://www.worldbank.org/projects/P144674?lang=en</td>\n",
       "    </tr>\n",
       "  </tbody>\n",
       "</table>\n",
       "<p>2 rows × 50 columns</p>\n",
       "</div>"
      ],
      "text/plain": [
       "                           _id approvalfy board_approval_month  \\\n",
       "0  (52b213b38594d8a2be17c780,)       1999             November   \n",
       "1  (52b213b38594d8a2be17c781,)       2015             November   \n",
       "\n",
       "      boardapprovaldate                                 borrower  \\\n",
       "0  2013-11-12T00:00:00Z  FEDERAL DEMOCRATIC REPUBLIC OF ETHIOPIA   \n",
       "1  2013-11-04T00:00:00Z                    GOVERNMENT OF TUNISIA   \n",
       "\n",
       "            closingdate                              country_namecode  \\\n",
       "0  2018-07-07T00:00:00Z  Federal Democratic Republic of Ethiopia!$!ET   \n",
       "1                  None                      Republic of Tunisia!$!TN   \n",
       "\n",
       "  countrycode                              countryname countryshortname  \\\n",
       "0          ET  Federal Democratic Republic of Ethiopia         Ethiopia   \n",
       "1          TN                      Republic of Tunisia          Tunisia   \n",
       "\n",
       "                         ...                           sectorcode source  \\\n",
       "0                        ...                          ET,BS,ES,EP   IBRD   \n",
       "1                        ...                                BZ,BS   IBRD   \n",
       "\n",
       "   status  supplementprojectflg                           theme1  \\\n",
       "0  Active                     N         (Education for all, 100)   \n",
       "1  Active                     N  (Other economic management, 30)   \n",
       "\n",
       "                                      theme_namecode themecode   totalamt  \\\n",
       "0                          [(65, Education for all)]        65  130000000   \n",
       "1  [(24, Other economic management), (54, Social ...     54,24          0   \n",
       "\n",
       "  totalcommamt                                                url  \n",
       "0    130000000  http://www.worldbank.org/projects/P129828/ethi...  \n",
       "1      4700000  http://www.worldbank.org/projects/P144674?lang=en  \n",
       "\n",
       "[2 rows x 50 columns]"
      ]
     },
     "execution_count": 8,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "#Extra credit, take the DataFrame you created with the two records and convert it into a Pandas DataFrame\n",
    "spark.sql(\"select * from world_bank limit 2\").toPandas()"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 9,
   "metadata": {
    "collapsed": false,
    "scrolled": true
   },
   "outputs": [
    {
     "data": {
      "text/html": [
       "<div>\n",
       "<table border=\"1\" class=\"dataframe\">\n",
       "  <thead>\n",
       "    <tr style=\"text-align: right;\">\n",
       "      <th></th>\n",
       "      <th>regionname</th>\n",
       "      <th>regioncount</th>\n",
       "    </tr>\n",
       "  </thead>\n",
       "  <tbody>\n",
       "    <tr>\n",
       "      <th>0</th>\n",
       "      <td>Africa</td>\n",
       "      <td>152</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>1</th>\n",
       "      <td>East Asia and Pacific</td>\n",
       "      <td>100</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>2</th>\n",
       "      <td>Europe and Central Asia</td>\n",
       "      <td>74</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>3</th>\n",
       "      <td>South Asia</td>\n",
       "      <td>65</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>4</th>\n",
       "      <td>Middle East and North Africa</td>\n",
       "      <td>54</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>5</th>\n",
       "      <td>Latin America and Caribbean</td>\n",
       "      <td>53</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>6</th>\n",
       "      <td>Other</td>\n",
       "      <td>2</td>\n",
       "    </tr>\n",
       "  </tbody>\n",
       "</table>\n",
       "</div>"
      ],
      "text/plain": [
       "                     regionname  regioncount\n",
       "0                        Africa          152\n",
       "1         East Asia and Pacific          100\n",
       "2       Europe and Central Asia           74\n",
       "3                    South Asia           65\n",
       "4  Middle East and North Africa           54\n",
       "5   Latin America and Caribbean           53\n",
       "6                         Other            2"
      ]
     },
     "execution_count": 9,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "# Now calculate a simple count based on a group, for example \"regionname\".   Return the regionname and a count of the values for that regionname. \n",
    "spark.sql(\"select regionname, count(*) as regioncount from world_bank group by regionname order by regioncount desc\").toPandas()"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 10,
   "metadata": {
    "collapsed": false
   },
   "outputs": [
    {
     "data": {
      "text/html": [
       "<div>\n",
       "<table border=\"1\" class=\"dataframe\">\n",
       "  <thead>\n",
       "    <tr style=\"text-align: right;\">\n",
       "      <th></th>\n",
       "      <th>Name</th>\n",
       "    </tr>\n",
       "  </thead>\n",
       "  <tbody>\n",
       "    <tr>\n",
       "      <th>0</th>\n",
       "      <td>[Primary education, Secondary education, Publi...</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>1</th>\n",
       "      <td>[Public administration- Other social services,...</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>2</th>\n",
       "      <td>[Rural and Inter-Urban Roads and Highways]</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>3</th>\n",
       "      <td>[Other social services]</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>4</th>\n",
       "      <td>[General industry and trade sector, Other indu...</td>\n",
       "    </tr>\n",
       "  </tbody>\n",
       "</table>\n",
       "</div>"
      ],
      "text/plain": [
       "                                                Name\n",
       "0  [Primary education, Secondary education, Publi...\n",
       "1  [Public administration- Other social services,...\n",
       "2         [Rural and Inter-Urban Roads and Highways]\n",
       "3                            [Other social services]\n",
       "4  [General industry and trade sector, Other indu..."
      ]
     },
     "execution_count": 10,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "# With JSON data you can reference the nested data.  \n",
    "# If you look at the Schema above you can see that sector.Name is a nested column.\n",
    "# Select that column and limit to a reasonable output (say five rows)\n",
    "spark.sql(\"select sector.Name from world_bank limit 5\").toPandas()"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "## Step 6 - Creating Simple Graphs\n",
    "<br>\n",
    "Create some simple graphs using the [matplotlib](http://matplotlib.org/1.5.3/index.html) and [numpy](http://www.numpy.org/) libraries\n",
    "<br>\n",
    "The \"%matplotlib inline\" statement is used to ensure that graphs are drawn within the notebook instead of popping up as separate windows.\n",
    "\n",
    "Make SURE you actually run this cell!"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 11,
   "metadata": {
    "collapsed": false
   },
   "outputs": [],
   "source": [
    "# Load the libraries\n",
    "%matplotlib inline \n",
    "import matplotlib.pyplot as plt, numpy as np"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {
    "collapsed": false
   },
   "source": [
    "### Step 6.1 - Create the SQL data\n",
    "Write the sql statement and look at the data, remember to add <i>.toPandas()</i> for a formatted display. An easier option is to create a variable and set it to the SQL statement.\n",
    "#### First create a SQL statement that is a reasonable number of items\n",
    "For example, you can count the number of projects (rows) by countryname\n",
    "<br>or in other words: \n",
    "<br>count(*), countryname from table group by countryname<br><br>\n",
    "\n",
    " <div class=\"panel-group\" id=\"accordion-61\">\n",
    "  <div class=\"panel panel-default\">\n",
    "    <div class=\"panel-heading\">\n",
    "      <h4 class=\"panel-title\">\n",
    "        <a data-toggle=\"collapse\" data-parent=\"#accordion-61\" href=\"#collapse1-61\">\n",
    "        Hint 1</a>\n",
    "      </h4>\n",
    "    </div>\n",
    "    <div id=\"collapse1-61\" class=\"panel-collapse collapse\">\n",
    "      <div class=\"panel-body\">Type:<br>\n",
    "query = \"select count(*) as Count, countryname from world_bank group by countryname\"<br></div>\n",
    "    </div>\n",
    "  </div>\n",
    "  <div class=\"panel panel-default\">\n",
    "    <div class=\"panel-heading\">\n",
    "      <h4 class=\"panel-title\">\n",
    "        <a data-toggle=\"collapse\" data-parent=\"#accordion-61\" href=\"#collapse2-61\">\n",
    "        Hint 2</a>\n",
    "      </h4>\n",
    "    </div>\n",
    "    <div id=\"collapse2-61\" class=\"panel-collapse collapse\">\n",
    "      <div class=\"panel-body\">Type:<br>\n",
    "      chart1_df = spark.sql(query).toPandas()<br>\n",
    "print chart1_df<br></div>\n",
    "    </div>\n",
    "  </div>\n",
    "  <div class=\"panel panel-default\">\n",
    "    <div class=\"panel-heading\">\n",
    "      <h4 class=\"panel-title\">\n",
    "        <a data-toggle=\"collapse\" data-parent=\"#accordion-61\" href=\"#collapse3-61\">\n",
    "        Advanced Optional 1</a>\n",
    "      </h4>\n",
    "    </div>\n",
    "    <div id=\"collapse3-61\" class=\"panel-collapse collapse\">\n",
    "      <div class=\"panel-body\">Printing the result isn't as nicely formatted.   What command gives you a nicely formatted output?   Use that instead.</div>\n",
    "    </div>\n",
    "  </div>\n",
    "</div> \n"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 12,
   "metadata": {
    "collapsed": false,
    "scrolled": true
   },
   "outputs": [
    {
     "name": "stdout",
     "output_type": "stream",
     "text": [
      "    Count                               countryname\n",
      "0      19                     Republic of Indonesia\n",
      "1       2                                South Asia\n",
      "2       4                        Republic of Turkey\n",
      "3       2                                     World\n",
      "4       4              Middle East and North Africa\n",
      "5       1                       Republic of Namibia\n",
      "6       2          Republic of the Marshall Islands\n",
      "7       5                       Republic of Liberia\n",
      "8       1                         Republic of Chile\n",
      "9       2                  Republic of Sierra Leone\n",
      "10      4                       Republic of Burundi\n",
      "11      4                         Republic of Benin\n",
      "12      6                          Republic of Peru\n",
      "13      4                    Republic of Azerbaijan\n",
      "14      7               Hashemite Kingdom of Jordan\n",
      "15      5                         Republic of Haiti\n",
      "16     11                                    Africa\n",
      "17      1                    Republic of Costa Rica\n",
      "18      3               Republic of the Philippines\n",
      "19      8                       Republic of Armenia\n",
      "20      5                         Republic of Niger\n",
      "21      1  Democratic Socialist Republic of Sri Lan\n",
      "22      2            Islamic Republic of Mauritania\n",
      "23      1                      Republic of Kiribati\n",
      "24      4                 Republic of Cote d'Ivoire\n",
      "25      4                           Pacific Islands\n",
      "26      2                      Republic of Cameroon\n",
      "27      1                                    Tuvalu\n",
      "28      8               United Republic of Tanzania\n",
      "29      2                     Republic of Guatemala\n",
      "30      3                        Kingdom of Lesotho\n",
      "31      2                       Kingdom of Cambodia\n",
      "32      1                     East Asia and Pacific\n",
      "33      3                      Republic of Djibouti\n",
      "34      2                        Republic of Malawi\n",
      "35      1                       Republic of Belarus\n",
      "36      3                          Republic of Togo\n",
      "37      9             Federative Republic of Brazil\n",
      "38      2                     Republic of Mauritius\n",
      "39      3          Republic of the Union of Myanmar\n"
     ]
    },
    {
     "data": {
      "text/html": [
       "<div>\n",
       "<table border=\"1\" class=\"dataframe\">\n",
       "  <thead>\n",
       "    <tr style=\"text-align: right;\">\n",
       "      <th></th>\n",
       "      <th>Count</th>\n",
       "      <th>countryname</th>\n",
       "    </tr>\n",
       "  </thead>\n",
       "  <tbody>\n",
       "    <tr>\n",
       "      <th>0</th>\n",
       "      <td>19</td>\n",
       "      <td>Republic of Indonesia</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>1</th>\n",
       "      <td>2</td>\n",
       "      <td>South Asia</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>2</th>\n",
       "      <td>4</td>\n",
       "      <td>Republic of Turkey</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>3</th>\n",
       "      <td>2</td>\n",
       "      <td>World</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>4</th>\n",
       "      <td>4</td>\n",
       "      <td>Middle East and North Africa</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>5</th>\n",
       "      <td>1</td>\n",
       "      <td>Republic of Namibia</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>6</th>\n",
       "      <td>2</td>\n",
       "      <td>Republic of the Marshall Islands</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>7</th>\n",
       "      <td>5</td>\n",
       "      <td>Republic of Liberia</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>8</th>\n",
       "      <td>1</td>\n",
       "      <td>Republic of Chile</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>9</th>\n",
       "      <td>2</td>\n",
       "      <td>Republic of Sierra Leone</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>10</th>\n",
       "      <td>4</td>\n",
       "      <td>Republic of Burundi</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>11</th>\n",
       "      <td>4</td>\n",
       "      <td>Republic of Benin</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>12</th>\n",
       "      <td>6</td>\n",
       "      <td>Republic of Peru</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>13</th>\n",
       "      <td>4</td>\n",
       "      <td>Republic of Azerbaijan</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>14</th>\n",
       "      <td>7</td>\n",
       "      <td>Hashemite Kingdom of Jordan</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>15</th>\n",
       "      <td>5</td>\n",
       "      <td>Republic of Haiti</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>16</th>\n",
       "      <td>11</td>\n",
       "      <td>Africa</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>17</th>\n",
       "      <td>1</td>\n",
       "      <td>Republic of Costa Rica</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>18</th>\n",
       "      <td>3</td>\n",
       "      <td>Republic of the Philippines</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>19</th>\n",
       "      <td>8</td>\n",
       "      <td>Republic of Armenia</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>20</th>\n",
       "      <td>5</td>\n",
       "      <td>Republic of Niger</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>21</th>\n",
       "      <td>1</td>\n",
       "      <td>Democratic Socialist Republic of Sri Lan</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>22</th>\n",
       "      <td>2</td>\n",
       "      <td>Islamic Republic of Mauritania</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>23</th>\n",
       "      <td>1</td>\n",
       "      <td>Republic of Kiribati</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>24</th>\n",
       "      <td>4</td>\n",
       "      <td>Republic of Cote d'Ivoire</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>25</th>\n",
       "      <td>4</td>\n",
       "      <td>Pacific Islands</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>26</th>\n",
       "      <td>2</td>\n",
       "      <td>Republic of Cameroon</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>27</th>\n",
       "      <td>1</td>\n",
       "      <td>Tuvalu</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>28</th>\n",
       "      <td>8</td>\n",
       "      <td>United Republic of Tanzania</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>29</th>\n",
       "      <td>2</td>\n",
       "      <td>Republic of Guatemala</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>30</th>\n",
       "      <td>3</td>\n",
       "      <td>Kingdom of Lesotho</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>31</th>\n",
       "      <td>2</td>\n",
       "      <td>Kingdom of Cambodia</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>32</th>\n",
       "      <td>1</td>\n",
       "      <td>East Asia and Pacific</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>33</th>\n",
       "      <td>3</td>\n",
       "      <td>Republic of Djibouti</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>34</th>\n",
       "      <td>2</td>\n",
       "      <td>Republic of Malawi</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>35</th>\n",
       "      <td>1</td>\n",
       "      <td>Republic of Belarus</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>36</th>\n",
       "      <td>3</td>\n",
       "      <td>Republic of Togo</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>37</th>\n",
       "      <td>9</td>\n",
       "      <td>Federative Republic of Brazil</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>38</th>\n",
       "      <td>2</td>\n",
       "      <td>Republic of Mauritius</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>39</th>\n",
       "      <td>3</td>\n",
       "      <td>Republic of the Union of Myanmar</td>\n",
       "    </tr>\n",
       "  </tbody>\n",
       "</table>\n",
       "</div>"
      ],
      "text/plain": [
       "    Count                               countryname\n",
       "0      19                     Republic of Indonesia\n",
       "1       2                                South Asia\n",
       "2       4                        Republic of Turkey\n",
       "3       2                                     World\n",
       "4       4              Middle East and North Africa\n",
       "5       1                       Republic of Namibia\n",
       "6       2          Republic of the Marshall Islands\n",
       "7       5                       Republic of Liberia\n",
       "8       1                         Republic of Chile\n",
       "9       2                  Republic of Sierra Leone\n",
       "10      4                       Republic of Burundi\n",
       "11      4                         Republic of Benin\n",
       "12      6                          Republic of Peru\n",
       "13      4                    Republic of Azerbaijan\n",
       "14      7               Hashemite Kingdom of Jordan\n",
       "15      5                         Republic of Haiti\n",
       "16     11                                    Africa\n",
       "17      1                    Republic of Costa Rica\n",
       "18      3               Republic of the Philippines\n",
       "19      8                       Republic of Armenia\n",
       "20      5                         Republic of Niger\n",
       "21      1  Democratic Socialist Republic of Sri Lan\n",
       "22      2            Islamic Republic of Mauritania\n",
       "23      1                      Republic of Kiribati\n",
       "24      4                 Republic of Cote d'Ivoire\n",
       "25      4                           Pacific Islands\n",
       "26      2                      Republic of Cameroon\n",
       "27      1                                    Tuvalu\n",
       "28      8               United Republic of Tanzania\n",
       "29      2                     Republic of Guatemala\n",
       "30      3                        Kingdom of Lesotho\n",
       "31      2                       Kingdom of Cambodia\n",
       "32      1                     East Asia and Pacific\n",
       "33      3                      Republic of Djibouti\n",
       "34      2                        Republic of Malawi\n",
       "35      1                       Republic of Belarus\n",
       "36      3                          Republic of Togo\n",
       "37      9             Federative Republic of Brazil\n",
       "38      2                     Republic of Mauritius\n",
       "39      3          Republic of the Union of Myanmar"
      ]
     },
     "metadata": {},
     "output_type": "display_data"
    }
   ],
   "source": [
    "# create the query to obtain the number of projects by countryname, save to a variable and print that variable\n",
    "query = \"select count(*) as Count, countryname from world_bank group by countryname limit 40\"\n",
    "chart1_df = spark.sql(query).toPandas()\n",
    "print chart1_df\n",
    "\n",
    "#Advanced Optional 1\n",
    "from IPython.display import display\n",
    "display(chart1_df)"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "### Step 6.2 - Create charts based on the SQL data\n",
    "<br>\n",
    "Here we wish to create a chart based on the SQL data we just obtained.   Python is an excellent choice when you need to create charts because of the variety and power of the charting libraries available.   The one we are using here is for Pandas.   Specifically the plot() method.   Documentation can be found <a href=\"http://pandas.pydata.org/pandas-docs/stable/generated/pandas.DataFrame.plot.html\">here</a>.\n",
    "\n",
    " <div class=\"panel-group\" id=\"accordion-62\">\n",
    "  <div class=\"panel panel-default\">\n",
    "    <div class=\"panel-heading\">\n",
    "      <h4 class=\"panel-title\">\n",
    "        <a data-toggle=\"collapse\" data-parent=\"#accordion-1\" href=\"#collapse1-62\">\n",
    "        Hint 1</a>\n",
    "      </h4>\n",
    "    </div>\n",
    "    <div id=\"collapse1-62\" class=\"panel-collapse collapse\">\n",
    "      <div class=\"panel-body\">Type:<br>\n",
    "      chart1_df.plot(kind='bar', x='countryname', y='Count', figsize=(12, 5))</div>\n",
    "    </div>\n",
    "  </div>\n",
    "  <div class=\"panel panel-default\">\n",
    "    <div class=\"panel-heading\">\n",
    "      <h4 class=\"panel-title\">\n",
    "        <a data-toggle=\"collapse\" data-parent=\"#accordion-62\" href=\"#collapse2-62\">\n",
    "       Advanced Optional 1</a>\n",
    "      </h4>\n",
    "    </div>\n",
    "    <div id=\"collapse2-62\" class=\"panel-collapse collapse\">\n",
    "      <div class=\"panel-body\">The table contains too much data.   Change the SQL statement to return a smaller group of values like 30 or 40<br></div>\n",
    "    </div>\n",
    "  </div>\n",
    "  <div class=\"panel panel-default\">\n",
    "    <div class=\"panel-heading\">\n",
    "      <h4 class=\"panel-title\">\n",
    "        <a data-toggle=\"collapse\" data-parent=\"#accordion-62\" href=\"#collapse3-62\">\n",
    "        Advanced Optional 2</a>\n",
    "      </h4>\n",
    "    </div>\n",
    "    <div id=\"collapse3-62\" class=\"panel-collapse collapse\">\n",
    "      <div class=\"panel-body\">Looking at the Pandas <i>plot()</i> documentation try other styles of plotting.   Look <a href=\"http://pandas.pydata.org/pandas-docs/version/0.18.1/visualization.html\">here</a> for ideas.<br></div>\n",
    "    </div>\n",
    "  </div>\n",
    "</div> \n"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 13,
   "metadata": {
    "collapsed": false
   },
   "outputs": [
    {
     "data": {
      "text/plain": [
       "<matplotlib.axes._subplots.AxesSubplot at 0x7f21623726d0>"
      ]
     },
     "execution_count": 13,
     "metadata": {},
     "output_type": "execute_result"
    },
    {
     "data": {
      "image/png": "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\n",
      "text/plain": [
       "<matplotlib.figure.Figure at 0x7f21710a3a10>"
      ]
     },
     "metadata": {},
     "output_type": "display_data"
    }
   ],
   "source": [
    "# Now take the variable (or same sql statement) and use the method:\n",
    "# .plot(kind='bar', x='countryname', y='Count', figsize=(12, 5)) to plot a graph\n",
    "\n",
    "chart1_df.plot(kind='bar', x='countryname', y='Count', figsize=(12, 5))\n",
    "#chart1_df.plot(kind='barh', x='countryname', y='Count', figsize=(12, 5))\n"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "## Step 7 - Creating a DataFrame\n",
    "<br>\n",
    "Not all data comes with a defined (or derivable) schema like JSON.   Sometimes we have the data first and <b>then</b> need to create a schema for it.<br>\n",
    "Try adding a schema to an RDD to create a DataFrame.<br>\n",
    "First, you need to create an RDD. This can be done with a loop or as\n",
    "seen in the instructor's example, or more simply by assigning values to an array.\n",
    "<br><br>"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 14,
   "metadata": {
    "collapsed": false
   },
   "outputs": [
    {
     "data": {
      "text/plain": [
       "[[1, 1, 1], [2, 2, 2], [3, 3, 3], ['4a', '4a', '4a'], [5, 5, 5]]"
      ]
     },
     "execution_count": 14,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "# Default array defined below. Feel free to change as desired.\n",
    "array=[[1,1,1],[2,2,2],[3,3,3],[\"4a\",\"4a\",\"4a\"],[5,5,5]]\n",
    "my_rdd = sc.parallelize(array)\n",
    "my_rdd.collect()"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "### Step 7.1 - Second, you need to add a schema to the RDD you created in the previous code block.\n",
    "Use first the StructField method, following these steps:<br>\n",
    "1- Define your schema columns as a string<br>\n",
    "2- Build the schema object using StructField<br>\n",
    "3- Apply the schema object to the RDD<br>\n",
    "\n",
    "Note: The cell below is missing some code and will not run properly until you add in some missing parts.\n",
    "<br><br>\n",
    "<div class=\"panel-group\" id=\"accordion-71\">\n",
    "  <div class=\"panel panel-default\">\n",
    "    <div class=\"panel-heading\">\n",
    "      <h4 class=\"panel-title\">\n",
    "        <a data-toggle=\"collapse\" data-parent=\"#accordion-71\" href=\"#collapse1-71\">\n",
    "        Hint 1</a>\n",
    "      </h4>\n",
    "    </div>\n",
    "    <div id=\"collapse1-71\" class=\"panel-collapse collapse\">\n",
    "      <div class=\"panel-body\">The schema string is simply the space-separated list of column names (i.e. \"var1 var2 var3\")<br></div>\n",
    "    </div>\n",
    "  </div>\n",
    "  <div class=\"panel panel-default\">\n",
    "    <div class=\"panel-heading\">\n",
    "      <h4 class=\"panel-title\">\n",
    "        <a data-toggle=\"collapse\" data-parent=\"#accordion-71\" href=\"#collapse2-71\">\n",
    "        Hint 2</a>\n",
    "      </h4>\n",
    "    </div>\n",
    "    <div id=\"collapse2-71\" class=\"panel-collapse collapse\">\n",
    "      <div class=\"panel-body\">The type should be IntegerType or StringType.   Note that because we are applying this is a loop *everything* will be an Integer or String<br></div>\n",
    "    </div>\n",
    "  </div>\n",
    "  <div class=\"panel panel-default\">\n",
    "    <div class=\"panel-heading\">\n",
    "      <h4 class=\"panel-title\">\n",
    "        <a data-toggle=\"collapse\" data-parent=\"#accordion-71\" href=\"#collapse3-71\">\n",
    "        Hint 3</a>\n",
    "      </h4>\n",
    "    </div>\n",
    "    <div id=\"collapse3-71\" class=\"panel-collapse collapse\">\n",
    "      <div class=\"panel-body\">Use the RDD you created above and apply the schema to it i.e.<br>\n",
    "      schemaExample = sqlContext.createDataFrame(my_rdd, schema)\n",
    "      </div>\n",
    "    </div>\n",
    "  </div>\n",
    "    <div class=\"panel panel-default\">\n",
    "    <div class=\"panel-heading\">\n",
    "      <h4 class=\"panel-title\">\n",
    "        <a data-toggle=\"collapse\" data-parent=\"#accordion-71\" href=\"#collapse4-71\">\n",
    "        Hint 4</a>\n",
    "      </h4>\n",
    "    </div>\n",
    "    <div id=\"collapse4-71\" class=\"panel-collapse collapse\">\n",
    "      <div class=\"panel-body\">We really don't need to tell you a name to use for your temp table do we?</div>\n",
    "    </div>\n",
    "  </div>\n",
    "</div> \n"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 15,
   "metadata": {
    "collapsed": true
   },
   "outputs": [],
   "source": [
    "from pyspark.sql.types import *\n",
    "\n",
    "# The schema is encoded in a string. Complete the string below\n",
    "schemaString = \"var1 var2 var3\"\n",
    "\n",
    "# MissingType() should be either StringType() or IntegerType(). Please replace as required.\n",
    "fields = [StructField(field_name, StringType(), True) for field_name in schemaString.split()]\n",
    "schema = StructType(fields)\n",
    "\n",
    "# Apply the schema to the RDD.\n",
    "schemaExample = spark.createDataFrame(my_rdd, schema)\n",
    "\n",
    "# Register the DataFrame as a table. Add table name below as parameter to registerTempTable.\n",
    "schemaExample.createTempView(\"myRDDTempTable\")\n"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "### Step 7.2 - Thirdly, write some SQL statements to verify that you successfully added a schema to your RDD\n",
    "<br>\n",
    " <div class=\"panel-group\" id=\"accordion-72\">\n",
    "  <div class=\"panel panel-default\">\n",
    "    <div class=\"panel-heading\">\n",
    "      <h4 class=\"panel-title\">\n",
    "        <a data-toggle=\"collapse\" data-parent=\"#accordion-72\" href=\"#collapse1-72\">\n",
    "        Hint 1</a>\n",
    "      </h4>\n",
    "    </div>\n",
    "    <div id=\"collapse1-72\" class=\"panel-collapse collapse\">\n",
    "      <div class=\"panel-body\">spark.sql(\"select * from myRDDTempTable\").toPandas()</div>\n",
    "    </div>\n",
    "  </div>\n",
    "  <div class=\"panel panel-default\">\n",
    "    <div class=\"panel-heading\">\n",
    "      <h4 class=\"panel-title\">\n",
    "        <a data-toggle=\"collapse\" data-parent=\"#accordion-72\" href=\"#collapse2-72\">\n",
    "        Advanced Optional 1</a>\n",
    "      </h4>\n",
    "    </div>\n",
    "    <div id=\"collapse2-72\" class=\"panel-collapse collapse\">\n",
    "      <div class=\"panel-body\">What is the type is changed to IntegerType (or StringType).   Any change in the results?</div>\n",
    "    </div>\n",
    "  </div>\n",
    "  <div class=\"panel panel-default\">\n",
    "    <div class=\"panel-heading\">\n",
    "      <h4 class=\"panel-title\">\n",
    "        <a data-toggle=\"collapse\" data-parent=\"#accordion-72\" href=\"#collapse3-72\">\n",
    "        Advanced Optional 2</a>\n",
    "      </h4>\n",
    "    </div>\n",
    "    <div id=\"collapse3-72\" class=\"panel-collapse collapse\">\n",
    "      <div class=\"panel-body\">Try to do some specific queries on the data (i.e.)<br>\n",
    "      spark.sql(\"select &#42; from myRDDTempTable where var3 > 2\").toPandas()<br>\n",
    "      Does this work regardless of the data type (i.e. IntegerType or StringType)?<br>\n",
    "      What if you change some of the input values (i.e. change all 4s to \"4a\")<br></div>\n",
    "    </div>\n",
    "  </div>\n",
    "</div> "
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 16,
   "metadata": {
    "collapsed": false
   },
   "outputs": [
    {
     "data": {
      "text/html": [
       "<div>\n",
       "<table border=\"1\" class=\"dataframe\">\n",
       "  <thead>\n",
       "    <tr style=\"text-align: right;\">\n",
       "      <th></th>\n",
       "      <th>var1</th>\n",
       "      <th>var2</th>\n",
       "      <th>var3</th>\n",
       "    </tr>\n",
       "  </thead>\n",
       "  <tbody>\n",
       "    <tr>\n",
       "      <th>0</th>\n",
       "      <td>3</td>\n",
       "      <td>3</td>\n",
       "      <td>3</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>1</th>\n",
       "      <td>5</td>\n",
       "      <td>5</td>\n",
       "      <td>5</td>\n",
       "    </tr>\n",
       "  </tbody>\n",
       "</table>\n",
       "</div>"
      ],
      "text/plain": [
       "  var1 var2 var3\n",
       "0    3    3    3\n",
       "1    5    5    5"
      ]
     },
     "execution_count": 16,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "#Run some SQL statements on your newly created DataFrame and display the output\n",
    "#spark.sql(\"select * from myRDDTempTable\").toPandas()\n",
    "spark.sql(\"select * from myRDDTempTable where var3 > 2\").toPandas()"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "## Step 8\n",
    "### Reading from an external data source\n",
    "If you have time, this is a good example to show you how to read from other datasources.  <br><br>\n",
    "In a different browser tab, create a dashDB service, add credentials and come back to this notebook. <br>If you are using Data Science Experience, you need to log into Bluemix and create a dashDB instance.   The login and password should be the same as for DSE.<br>\n",
    "Each dashDB instance in Bluemix is created with a \"GOSALES\" set of tables which we can reuse for the purpose of this example. (You can create your own tables if you wish...)<br><br>Replace the Xs in the cell below with proper credentials and verify access to dashDB tables.<br><br>\n",
    "You can read from any database that you can connect to through jdbc.  Here is the [documentation](http://spark.apache.org/docs/latest/sql-programming-guide.html#jdbc-to-other-databases)\n",
    "<br><br>\n",
    " <div class=\"panel-group\" id=\"accordion-8\">\n",
    "  <div class=\"panel panel-default\">\n",
    "    <div class=\"panel-heading\">\n",
    "      <h4 class=\"panel-title\">\n",
    "        <a data-toggle=\"collapse\" data-parent=\"#accordion-8\" href=\"#collapse1-8\">\n",
    "        Hint 1</a>\n",
    "      </h4>\n",
    "    </div>\n",
    "    <div id=\"collapse1-8\" class=\"panel-collapse collapse\">\n",
    "      <div class=\"panel-body\">To connect to a general dashDB instance:<br>\n",
    "      url=\"\"<br>\n",
    "user=\"\"<br>\n",
    "password=\"\"<br>\n",
    "connection=\"jdbc:db2://\" + url + \":50000/BLUDB:user=\" + user + \";password=\" + password + \";\"<br></div>\n",
    "    </div>\n",
    "  </div>\n",
    "  <div class=\"panel panel-default\">\n",
    "    <div class=\"panel-heading\">\n",
    "      <h4 class=\"panel-title\">\n",
    "        <a data-toggle=\"collapse\" data-parent=\"#accordion-8\" href=\"#collapse2-8\">\n",
    "        Advanced Optional</a>\n",
    "      </h4>\n",
    "    </div>\n",
    "    <div id=\"collapse2-8\" class=\"panel-collapse collapse\">\n",
    "      <div class=\"panel-body\">Create your own dashDB instance in Bluemix and connect to it</div>\n",
    "    </div>\n",
    "  </div>\n",
    "</div> \n"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": null,
   "metadata": {
    "collapsed": false
   },
   "outputs": [],
   "source": [
    "url=\"\"\n",
    "user=\"\"\n",
    "password=\"\"\n",
    "connection=\"jdbc:db2://\" + url + \":50000/BLUDB:user=\" + user + \";password=\" + password + \";\"\n",
    "\n",
    "salesDF = spark.read.format('jdbc').\\\n",
    "          options(url=connection,\\\n",
    "                  dbtable='GOSALES.BRANCH').load()\n",
    "salesDF.show()"
   ]
  }
 ],
 "metadata": {
  "kernelspec": {
   "display_name": "Python 2 with Spark 2.0",
   "language": "python",
   "name": "python2-spark20"
  },
  "language_info": {
   "codemirror_mode": {
    "name": "ipython",
    "version": 2
   },
   "file_extension": ".py",
   "mimetype": "text/x-python",
   "name": "python",
   "nbconvert_exporter": "python",
   "pygments_lexer": "ipython2",
   "version": "2.7.11"
  }
 },
 "nbformat": 4,
 "nbformat_minor": 0
}
{
 "cells": [
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "# Lab 3 - Spark MLlib\n",
    "\n",
    "\"A computer program is said to learn from experience E with respect to some class of tasks T and performance measure P if its performance at tasks in T, as measured by P, improves with experience E\"\n",
    "-Tom M. Mitchell\n",
    "\n",
    "Machine Learning - the science of getting computers to act without being explicitly programmed\n",
    "\n",
    "MLlib is Spark’s machine learning (ML) library. Its goal is to make practical machine learning scalable and easy. It consists of common learning algorithms and utilities, including classification, regression, clustering, collaborative filtering (this example!), dimensionality reduction, as well as lower-level optimization primitives and higher-level pipeline APIs.\n",
    "\n",
    "It divides into two packages:\n",
    "1. spark.mllib contains the original API built on top of RDDs.\n",
    "2. spark.ml provides higher-level API built on top of DataFrames for constructing ML pipelines.\n",
    "\n",
    "\n",
    "Using spark.ml is recommended because with DataFrames the API is more versatile and flexible. But we will keep supporting spark.mllib along with the development of spark.ml. Users should be comfortable using spark.mllib features and expect more features coming.\n",
    "\n",
    "http://spark.apache.org/docs/latest/mllib-guide.html\n",
    "\n",
    "## Online Purchase Recommendations\n",
    "\n",
    "Learn how to create a recommendation engine using the Alternating Least Squares algorithm in Spark's machine learning library\n",
    "\n",
    "<img src='https://raw.githubusercontent.com/rosswlewis/RecommendationPoT/master/ALS.png' width=\"70%\" height=\"70%\"></img>\n",
    "\n",
    "## The data\n",
    "\n",
    "This is a transnational data set which contains all the transactions occurring between 01/12/2010 and 09/12/2011 for a UK-based and registered non-store online retail.  The company mainly sells unique all-occasion gifts. Many customers of the company are wholesalers.\n",
    "\n",
    "http://archive.ics.uci.edu/ml/datasets/Online+Retail\n",
    "\n",
    "<img src='https://raw.githubusercontent.com/rosswlewis/RecommendationPoT/master/FullFile.png' width=\"80%\" height=\"80%\"></img>"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "## Step 1 - Create an RDD from the CSV File \n",
    "### 1.1 - Download the data"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 1,
   "metadata": {
    "collapsed": false,
    "scrolled": false
   },
   "outputs": [
    {
     "name": "stdout",
     "output_type": "stream",
     "text": [
      "--2016-11-15 11:22:48--  https://raw.githubusercontent.com/rosswlewis/RecommendationPoT/master/OnlineRetail.csv.gz\n",
      "Resolving raw.githubusercontent.com (raw.githubusercontent.com)... 151.101.48.133\n",
      "Connecting to raw.githubusercontent.com (raw.githubusercontent.com)|151.101.48.133|:443... connected.\n",
      "HTTP request sent, awaiting response... 200 OK\n",
      "Length: 7483128 (7.1M) [application/octet-stream]\n",
      "Saving to: 'OnlineRetail.csv.gz'\n",
      "\n",
      "100%[======================================>] 7,483,128   --.-K/s   in 0.1s    \n",
      "\n",
      "2016-11-15 11:22:48 (61.3 MB/s) - 'OnlineRetail.csv.gz' saved [7483128/7483128]\n",
      "\n"
     ]
    }
   ],
   "source": [
    "#Download the data from github to the local directory\n",
    "!rm 'OnlineRetail.csv.gz' -f\n",
    "!wget https://raw.githubusercontent.com/rosswlewis/RecommendationPoT/master/OnlineRetail.csv.gz"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "### 1.2 - Put the csv into an RDD (at first, each row in the RDD is a string which correlates to a line in the csv) and show the first three lines.\n",
    "<br>\n",
    " <div class=\"panel-group\" id=\"accordion-12\">\n",
    "  <div class=\"panel panel-default\">\n",
    "    <div class=\"panel-heading\">\n",
    "      <h4 class=\"panel-title\">\n",
    "        <a data-toggle=\"collapse\" data-parent=\"#accordion-1\" href=\"#collapse1-12\">\n",
    "        Hint 1</a>\n",
    "      </h4>\n",
    "    </div>\n",
    "    <div id=\"collapse1-12\" class=\"panel-collapse collapse\">\n",
    "      <div class=\"panel-body\">Use the Spark context (sc) to get the list of possible methods.  <i>sc.&lt;TAB&gt;</i></div>\n",
    "    </div>\n",
    "  </div>\n",
    "  <div class=\"panel panel-default\">\n",
    "    <div class=\"panel-heading\">\n",
    "      <h4 class=\"panel-title\">\n",
    "        <a data-toggle=\"collapse\" data-parent=\"#accordion-12\" href=\"#collapse2-12\">\n",
    "        Hint 2</a>\n",
    "      </h4>\n",
    "    </div>\n",
    "    <div id=\"collapse2-12\" class=\"panel-collapse collapse\">\n",
    "      <div class=\"panel-body\">Use the <i>textFile()</i> method</div>\n",
    "    </div>\n",
    "  </div>\n",
    "  <div class=\"panel panel-default\">\n",
    "    <div class=\"panel-heading\">\n",
    "      <h4 class=\"panel-title\">\n",
    "        <a data-toggle=\"collapse\" data-parent=\"#accordion-12\" href=\"#collapse3-12\">\n",
    "        Hint 3</a>\n",
    "      </h4>\n",
    "    </div>\n",
    "    <div id=\"collapse3-12\" class=\"panel-collapse collapse\">\n",
    "      <div class=\"panel-body\">Type:<br>\n",
    "loadRetailData = sc.textFile(\"OnlineRetail.csv.gz\")<br>\n",
    "loadRetailData.take(3)<br></div>\n",
    "    </div>\n",
    "  </div>\n",
    "</div> \n",
    "\n"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 2,
   "metadata": {
    "collapsed": false
   },
   "outputs": [
    {
     "data": {
      "text/plain": [
       "[u'InvoiceNo,StockCode,Description,Quantity,InvoiceDate,UnitPrice,CustomerID,Country',\n",
       " u'536365,85123A,WHITE HANGING HEART T-LIGHT HOLDER,6,12/1/10 8:26,2.55,17850,United Kingdom',\n",
       " u'536365,71053,WHITE METAL LANTERN,6,12/1/10 8:26,3.39,17850,United Kingdom']"
      ]
     },
     "execution_count": 2,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "loadRetailData = sc.textFile(\"OnlineRetail.csv.gz\")\n",
    "loadRetailData.take(3)"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "## Step 2 - Prepare and shape the data:  \"80% of a Data Scientists  job\""
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "### 2.1 - Remove the header from the RDD and split the remaining lines by comma.\n",
    "<br>\n",
    " <div class=\"panel-group\" id=\"accordion-21\">\n",
    "  <div class=\"panel panel-default\">\n",
    "    <div class=\"panel-heading\">\n",
    "      <h4 class=\"panel-title\">\n",
    "        <a data-toggle=\"collapse\" data-parent=\"#accordion-21\" href=\"#collapse1-21\">\n",
    "        Hint 1</a>\n",
    "      </h4>\n",
    "    </div>\n",
    "    <div id=\"collapse1-21\" class=\"panel-collapse collapse\">\n",
    "      <div class=\"panel-body\">The header is the first line in the RDD -- use <i>first()</i> to obtain it.</div>\n",
    "    </div>\n",
    "  </div>\n",
    "  <div class=\"panel panel-default\">\n",
    "    <div class=\"panel-heading\">\n",
    "      <h4 class=\"panel-title\">\n",
    "        <a data-toggle=\"collapse\" data-parent=\"#accordion-21\" href=\"#collapse2-21\">\n",
    "        Hint 2</a>\n",
    "      </h4>\n",
    "    </div>\n",
    "    <div id=\"collapse2-21\" class=\"panel-collapse collapse\">\n",
    "      <div class=\"panel-body\">Use the <i>filter()</i> method to filter out all lines which are not equal to the header line.</div>\n",
    "    </div>\n",
    "  </div>\n",
    "  <div class=\"panel panel-default\">\n",
    "    <div class=\"panel-heading\">\n",
    "      <h4 class=\"panel-title\">\n",
    "        <a data-toggle=\"collapse\" data-parent=\"#accordion-21\" href=\"#collapse3-21\">\n",
    "        Hint 3</a>\n",
    "      </h4>\n",
    "    </div>\n",
    "    <div id=\"collapse3-21\" class=\"panel-collapse collapse\">\n",
    "      <div class=\"panel-body\">Map the <i>split()</i> method to the remaining lines to split on \",\"</div>\n",
    "    </div>\n",
    "  </div>\n",
    "  <div class=\"panel panel-default\">\n",
    "    <div class=\"panel-heading\">\n",
    "      <h4 class=\"panel-title\">\n",
    "        <a data-toggle=\"collapse\" data-parent=\"#accordion-21\" href=\"#collapse4-21\">\n",
    "        Hint 4</a>\n",
    "      </h4>\n",
    "    </div>\n",
    "    <div id=\"collapse4-21\" class=\"panel-collapse collapse\">\n",
    "      <div class=\"panel-body\">Type:<br>\n",
    "\n",
    "header = loadRetailData.first()<br>\n",
    "splitColumns = loadRetailData.filter(lambda line: line != header).map(lambda l: l.split(\",\"))</div>\n",
    "    </div>\n",
    "  </div>\n",
    "</div> "
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 3,
   "metadata": {
    "collapsed": false
   },
   "outputs": [],
   "source": [
    "header = loadRetailData.first()\n",
    "splitColumns = loadRetailData.filter(lambda line: line != header).map(lambda l: l.split(\",\"))"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "### 2.2 - Filter the remaining lines using <a href=\"https://docs.python.org/2.6/howto/regex.html\">regular expressions</a>\n",
    "The original file at UCI's Machine Learning Repository has commas in the product description.  Those have been removed to expediate the lab.\n",
    "Only keep rows that have a quantity greater than 0, a non-empty customerID, and a non-blank stock code after removing non-numeric characters.<br><br>\n",
    " <div class=\"panel-group\" id=\"accordion-22\">\n",
    "  <div class=\"panel panel-default\">\n",
    "    <div class=\"panel-heading\">\n",
    "      <h4 class=\"panel-title\">\n",
    "        <a data-toggle=\"collapse\" data-parent=\"#accordion-22\" href=\"#collapse1-22\">\n",
    "        Hint 1</a>\n",
    "      </h4>\n",
    "    </div>\n",
    "    <div id=\"collapse1-22\" class=\"panel-collapse collapse\">\n",
    "      <div class=\"panel-body\">Examine the header to determine which fields need to be used to filter the data.</div>\n",
    "    </div>\n",
    "  </div>\n",
    "  <div class=\"panel panel-default\">\n",
    "    <div class=\"panel-heading\">\n",
    "      <h4 class=\"panel-title\">\n",
    "        <a data-toggle=\"collapse\" data-parent=\"#accordion-22\" href=\"#collapse2-22\">\n",
    "        Hint 2</a>\n",
    "      </h4>\n",
    "    </div>\n",
    "    <div id=\"collapse2-22\" class=\"panel-collapse collapse\">\n",
    "      <div class=\"panel-body\">Use the <i>filter()</i> method for the first two requirements.   Note -- you may have to cast values.</div>\n",
    "    </div>\n",
    "  </div>\n",
    "  <div class=\"panel panel-default\">\n",
    "    <div class=\"panel-heading\">\n",
    "      <h4 class=\"panel-title\">\n",
    "        <a data-toggle=\"collapse\" data-parent=\"#accordion-22\" href=\"#collapse3-22\">\n",
    "        Hint 3</a>\n",
    "      </h4>\n",
    "    </div>\n",
    "    <div id=\"collapse3-22\" class=\"panel-collapse collapse\">\n",
    "      <div class=\"panel-body\">Look at the <i><a href=\"https://docs.python.org/2.6/howto/regex.html\">re.sub()</a></i> method</div>\n",
    "    </div>\n",
    "  </div>\n",
    "  <div class=\"panel panel-default\">\n",
    "    <div class=\"panel-heading\">\n",
    "      <h4 class=\"panel-title\">\n",
    "        <a data-toggle=\"collapse\" data-parent=\"#accordion-22\" href=\"#collapse4-22\">\n",
    "        Hint 4</a>\n",
    "      </h4>\n",
    "    </div>\n",
    "    <div id=\"collapse4-22\" class=\"panel-collapse collapse\">\n",
    "      <div class=\"panel-body\">Type:<br>\n",
    "import re<br>\n",
    "filteredRetailData = splitColumns.filter(lambda l: int(l[3]) > 0 and len(re.sub(\"\\D\", \"\", l[1])) != 0 and l[6] != \"\")</div>\n",
    "    </div>\n",
    "  </div>\n",
    "</div> "
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 4,
   "metadata": {
    "collapsed": false
   },
   "outputs": [],
   "source": [
    "import re\n",
    "filteredRetailData = splitColumns.filter(lambda l: int(l[3]) > 0 and len(re.sub(\"\\D\", \"\", l[1])) != 0 and l[6] != \"\")"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "###  2.3 - Map each line to a SQL Row and create a Dataframe from the result.   Register the Dataframe as an SQL temp view.\n",
    "<br>\n",
    "Use the following for the Row column names: inv, stockCode, description, quant, invDate, price, custId, country.   inv, stockCode, quant and custId should be integers.   \n",
    "price is a float.  description and country are strings (the default).\n",
    "<br><br>\n",
    "Hint: When you replaced non-digit characters using the regular expression above, you replaced them in the context of a test.  You'll have to do it again when creating the stockCode Row value.\n",
    "<br><br>\n",
    " <div class=\"panel-group\" id=\"accordion-23\">\n",
    "  <div class=\"panel panel-default\">\n",
    "    <div class=\"panel-heading\">\n",
    "      <h4 class=\"panel-title\">\n",
    "        <a data-toggle=\"collapse\" data-parent=\"#accordion-23\" href=\"#collapse1-23\">\n",
    "        Hint 1</a>\n",
    "      </h4>\n",
    "    </div>\n",
    "    <div id=\"collapse1-23\" class=\"panel-collapse collapse\">\n",
    "      <div class=\"panel-body\">We haven't used SparkSession or Row in this notebook, so you will have to import them from the pyspark.sql package and then create a <i>SparkSession</i>.</div>\n",
    "    </div>\n",
    "  </div>\n",
    "  <div class=\"panel panel-default\">\n",
    "    <div class=\"panel-heading\">\n",
    "      <h4 class=\"panel-title\">\n",
    "        <a data-toggle=\"collapse\" data-parent=\"#accordion-23\" href=\"#collapse2-23\">\n",
    "        Hint 2</a>\n",
    "      </h4>\n",
    "    </div>\n",
    "    <div id=\"collapse2-23\" class=\"panel-collapse collapse\">\n",
    "      <div class=\"panel-body\">You can create a <i>Row</i> using a <i>map()</i>.   For example:<br>\n",
    "      example = myRDD.map(lambda x: Row(v1=x[1], v2=int(x[2]), v3=float(x[3]))<br>\n",
    "      Note how we set the column names this way.</div>\n",
    "    </div>\n",
    "  </div>\n",
    "  <div class=\"panel panel-default\">\n",
    "    <div class=\"panel-heading\">\n",
    "      <h4 class=\"panel-title\">\n",
    "        <a data-toggle=\"collapse\" data-parent=\"#accordion-23\" href=\"#collapse3-23\">\n",
    "        Hint 3</a>\n",
    "      </h4>\n",
    "    </div>\n",
    "    <div id=\"collapse3-23\" class=\"panel-collapse collapse\">\n",
    "      <div class=\"panel-body\">use <i>createDataFrame()</i> in your <i>SparkSession</i>.   Then register the dataframe with <i>createTempView()</i></div>\n",
    "    </div>\n",
    "  </div>\n",
    "  <div class=\"panel panel-default\">\n",
    "    <div class=\"panel-heading\">\n",
    "      <h4 class=\"panel-title\">\n",
    "        <a data-toggle=\"collapse\" data-parent=\"#accordion-23\" href=\"#collapse4-23\">\n",
    "        Hint 4</a>\n",
    "      </h4>\n",
    "    </div>\n",
    "    <div id=\"collapse4-23\" class=\"panel-collapse collapse\">\n",
    "      <div class=\"panel-body\">Type:<br>\n",
    "from pyspark.sql import SparkSession, Row<br>\n",
    "spark = SparkSession.builder.getOrCreate()<br>\n",
    "\n",
    "retailRows = filteredRetailData.map(lambda l: Row(inv=int(l[0]), stockCode=int(re.sub(\"\\D\", \"\", l[1])), description=l[2], quant=int(l[3]), invDate=l[4], price=float(l[5]), custId=int(l[6]), country=l[7]))<br>\n",
    "\n",
    "retailDf = spark.createDataFrame(retailRows)<br>\n",
    "retailDf.createTempView(\"retailPurchases\")</div>\n",
    "    </div>\n",
    "  </div>\n",
    "</div> "
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 5,
   "metadata": {
    "collapsed": false
   },
   "outputs": [
    {
     "data": {
      "text/html": [
       "<div>\n",
       "<table border=\"1\" class=\"dataframe\">\n",
       "  <thead>\n",
       "    <tr style=\"text-align: right;\">\n",
       "      <th></th>\n",
       "      <th>country</th>\n",
       "      <th>custId</th>\n",
       "      <th>description</th>\n",
       "      <th>inv</th>\n",
       "      <th>invDate</th>\n",
       "      <th>price</th>\n",
       "      <th>quant</th>\n",
       "      <th>stockCode</th>\n",
       "    </tr>\n",
       "  </thead>\n",
       "  <tbody>\n",
       "    <tr>\n",
       "      <th>0</th>\n",
       "      <td>United Kingdom</td>\n",
       "      <td>13901</td>\n",
       "      <td>DECORATIVE HANGING SHELVING UNIT</td>\n",
       "      <td>541990</td>\n",
       "      <td>1/25/11 9:01</td>\n",
       "      <td>59.95</td>\n",
       "      <td>1</td>\n",
       "      <td>84632</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>1</th>\n",
       "      <td>United Kingdom</td>\n",
       "      <td>16638</td>\n",
       "      <td>DECORATIVE HANGING SHELVING UNIT</td>\n",
       "      <td>545704</td>\n",
       "      <td>3/7/11 8:30</td>\n",
       "      <td>59.95</td>\n",
       "      <td>2</td>\n",
       "      <td>84632</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>2</th>\n",
       "      <td>United Kingdom</td>\n",
       "      <td>15696</td>\n",
       "      <td>DECORATIVE HANGING SHELVING UNIT</td>\n",
       "      <td>548038</td>\n",
       "      <td>3/29/11 12:03</td>\n",
       "      <td>59.95</td>\n",
       "      <td>1</td>\n",
       "      <td>84632</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>3</th>\n",
       "      <td>United Kingdom</td>\n",
       "      <td>17663</td>\n",
       "      <td>DECORATIVE HANGING SHELVING UNIT</td>\n",
       "      <td>559420</td>\n",
       "      <td>7/8/11 11:52</td>\n",
       "      <td>59.95</td>\n",
       "      <td>1</td>\n",
       "      <td>84632</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>4</th>\n",
       "      <td>United Kingdom</td>\n",
       "      <td>17175</td>\n",
       "      <td>DECORATIVE HANGING SHELVING UNIT</td>\n",
       "      <td>560914</td>\n",
       "      <td>7/21/11 18:08</td>\n",
       "      <td>59.95</td>\n",
       "      <td>1</td>\n",
       "      <td>84632</td>\n",
       "    </tr>\n",
       "  </tbody>\n",
       "</table>\n",
       "</div>"
      ],
      "text/plain": [
       "          country  custId                       description     inv  \\\n",
       "0  United Kingdom   13901  DECORATIVE HANGING SHELVING UNIT  541990   \n",
       "1  United Kingdom   16638  DECORATIVE HANGING SHELVING UNIT  545704   \n",
       "2  United Kingdom   15696  DECORATIVE HANGING SHELVING UNIT  548038   \n",
       "3  United Kingdom   17663  DECORATIVE HANGING SHELVING UNIT  559420   \n",
       "4  United Kingdom   17175  DECORATIVE HANGING SHELVING UNIT  560914   \n",
       "\n",
       "         invDate  price  quant  stockCode  \n",
       "0   1/25/11 9:01  59.95      1      84632  \n",
       "1    3/7/11 8:30  59.95      2      84632  \n",
       "2  3/29/11 12:03  59.95      1      84632  \n",
       "3   7/8/11 11:52  59.95      1      84632  \n",
       "4  7/21/11 18:08  59.95      1      84632  "
      ]
     },
     "execution_count": 5,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "from pyspark.sql import SparkSession, Row\n",
    "spark = SparkSession.builder.getOrCreate()\n",
    "retailRows = filteredRetailData.map(lambda l: Row(inv=int(l[0]), stockCode=int(re.sub(\"\\D\", \"\", l[1])), description=l[2], quant=int(l[3]), invDate=l[4], price=float(l[5]), custId=int(l[6]), country=l[7]))\n",
    "retailDf = spark.createDataFrame(retailRows)\n",
    "retailDf.createTempView(\"retailPurchases\")\n",
    "values = spark.sql(\"select * from retailPurchases where stockCode='84632'\")\n",
    "values.toPandas()"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "### 2.4 - Keep only the data we need (custId, stockCode, and rank)\n",
    "<br>\n",
    "The Alternating Least Squares algorithm requires three values and only three values.   In this case, we're going to use the Customer ID (custId), stock code (stockCode), and a ranking value.   In this situation there is not a ranking value within the data, so we will create one.   We will set a value of 1 to indicate a purchase since these are all actual orders.   Set that value to \"purch\".\n",
    "<br><br>\n",
    "After doing the select, group by custId and stockCode.\n",
    "<br><br>\n",
    " <div class=\"panel-group\" id=\"accordion-24\">\n",
    "  <div class=\"panel panel-default\">\n",
    "    <div class=\"panel-heading\">\n",
    "      <h4 class=\"panel-title\">\n",
    "        <a data-toggle=\"collapse\" data-parent=\"#accordion-24\" href=\"#collapse1-24\">\n",
    "        Hint 1</a>\n",
    "      </h4>\n",
    "    </div>\n",
    "    <div id=\"collapse1-24\" class=\"panel-collapse collapse\">\n",
    "      <div class=\"panel-body\">To add a fixed value within a select statement, use something like <i>select x,y,1 as purch from z</i></div>\n",
    "    </div>\n",
    "  </div>\n",
    "  <div class=\"panel panel-default\">\n",
    "    <div class=\"panel-heading\">\n",
    "      <h4 class=\"panel-title\">\n",
    "        <a data-toggle=\"collapse\" data-parent=\"#accordion-24\" href=\"#collapse2-24\">\n",
    "        Hint 2</a>\n",
    "      </h4>\n",
    "    </div>\n",
    "    <div id=\"collapse2-24\" class=\"panel-collapse collapse\">\n",
    "      <div class=\"panel-body\">Use the <i>group by</i> statement to group results.  To group by two values, separate them by commas (i.e. <i>group by x,y</i>)</div>\n",
    "    </div>\n",
    "  </div>\n",
    "  <div class=\"panel panel-default\">\n",
    "    <div class=\"panel-heading\">\n",
    "      <h4 class=\"panel-title\">\n",
    "        <a data-toggle=\"collapse\" data-parent=\"#accordion-24\" href=\"#collapse3-24\">\n",
    "        Hint 3</a>\n",
    "      </h4>\n",
    "    </div>\n",
    "    <div id=\"collapse3-24\" class=\"panel-collapse collapse\">\n",
    "      <div class=\"panel-body\">Type:\n",
    "\n",
    "query = \"\n",
    "SELECT \n",
    "    custId, stockCode, 1 as purch\n",
    "FROM \n",
    "    retailPurchases \n",
    "group \n",
    "    by custId, stockCode\"<br>\n",
    "uniqueCombDf = spark.sql(query)</div>\n",
    "    </div>\n",
    "  </div>\n",
    "</div> "
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 6,
   "metadata": {
    "collapsed": false
   },
   "outputs": [],
   "source": [
    "query = \" SELECT custId, stockCode, 1 as purch FROM retailPurchases group by custId, stockCode\"\n",
    "uniqueCombDf = spark.sql(query)"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "### 2.5 - Randomly split the data into a testing set (10% of the data), a cross validation set (10% of the data) a training set (80% of the data)\n",
    "<br><br>\n",
    "We wish to split up the data into three parts.   A training set (80%) to train the algorithm, a testing set (10%) and a cross-validation set (10%).   The data for each set should be randomly selected.\n",
    "<br><br>\n",
    " <div class=\"panel-group\" id=\"accordion-25\">\n",
    "  <div class=\"panel panel-default\">\n",
    "    <div class=\"panel-heading\">\n",
    "      <h4 class=\"panel-title\">\n",
    "        <a data-toggle=\"collapse\" data-parent=\"#accordion-25\" href=\"#collapse1-25\">\n",
    "        Hint 1</a>\n",
    "      </h4>\n",
    "    </div>\n",
    "    <div id=\"collapse1-25\" class=\"panel-collapse collapse\">\n",
    "      <div class=\"panel-body\">Use the <i><a href=\"https://spark.apache.org/docs/1.6.2/api/python/pyspark.sql.html#pyspark.sql.DataFrame.randomSplit\">randomSplit()</a></i> method</div>\n",
    "    </div>\n",
    "  </div>\n",
    "  <div class=\"panel panel-default\">\n",
    "    <div class=\"panel-heading\">\n",
    "      <h4 class=\"panel-title\">\n",
    "        <a data-toggle=\"collapse\" data-parent=\"#accordion-25\" href=\"#collapse2-25\">\n",
    "        Hint 2</a>\n",
    "      </h4>\n",
    "    </div>\n",
    "    <div id=\"collapse2-25\" class=\"panel-collapse collapse\">\n",
    "      <div class=\"panel-body\">Type:<br>\n",
    "      testDf, cvDf, trainDf = uniqueCombDf.randomSplit([.1,.1,.8])<br></div>\n",
    "    </div>\n",
    "  </div>\n",
    "  <div class=\"panel panel-default\">\n",
    "    <div class=\"panel-heading\">\n",
    "      <h4 class=\"panel-title\">\n",
    "        <a data-toggle=\"collapse\" data-parent=\"#accordion-25\" href=\"#collapse3-25\">\n",
    "        Advanced Optional 1</a>\n",
    "      </h4>\n",
    "    </div>\n",
    "    <div id=\"collapse3-25\" class=\"panel-collapse collapse\">\n",
    "      <div class=\"panel-body\"><i>randomSplit()</i> takes an optional seed parameter.  At the end of the exercise give a random seed and see whether the results change.</div>\n",
    "    </div>\n",
    "  </div>\n",
    "</div> "
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 7,
   "metadata": {
    "collapsed": false
   },
   "outputs": [],
   "source": [
    "testDf, cvDf, trainDf = uniqueCombDf.randomSplit([.1,.1,.8])"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "## Step 3 - Build recommendation models\n",
    "\n",
    "### 3.1 - Use the training dataframe to train a model with Alternating Least Squares using the <i><a href=\"https://spark.apache.org/docs/1.6.1/api/python/pyspark.ml.html#pyspark.ml.recommendation.ALS\">ALS</a></i> class\n",
    "<br>\n",
    "ALS attempts to estimate the ratings matrix R as the product of two lower-rank matrices, X and Y, i.e. X * Yt = R. Typically these approximations are called ‘factor’ matrices. The general approach is iterative. During each iteration, one of the factor matrices is held constant, while the other is solved for using least squares. The newly-solved factor matrix is then held constant while solving for the other factor matrix.\n",
    "<br><br>\n",
    "Latent Factors / rank<br>\n",
    "&nbsp;&nbsp;&nbsp;&nbsp;The number of columns in the user-feature and product-feature matricies<br>\n",
    "Iterations / maxIter<br>\n",
    "&nbsp;&nbsp;&nbsp;&nbsp;The number of factorization runs<br><br>\n",
    "To use the ALS class type:\n",
    "<br>\n",
    "from pyspark.ml.recommendation import ALS<br>\n",
    "<br>\n",
    "When running ALS, we need to create two separate instances.   For both instances userCol is custId, itemCol is stockCode and ratingCol is purch.<br><br>\n",
    "For the first instance, use a rank of 15 and set iterations to 5.<br>\n",
    "For the second instance, use a rank of 2 and set iterations to 10.<br>\n",
    "Run <i><a href=\"https://spark.apache.org/docs/1.6.1/api/python/pyspark.ml.html#pyspark.ml.recommendation.ALS.fit\">fit()</a></i> on both instances using the training dataframe.<br>\n",
    "<br>\n",
    " <div class=\"panel-group\" id=\"accordion-31\">\n",
    "  <div class=\"panel panel-default\">\n",
    "    <div class=\"panel-heading\">\n",
    "      <h4 class=\"panel-title\">\n",
    "        <a data-toggle=\"collapse\" data-parent=\"#accordion-31\" href=\"#collapse1-31\">\n",
    "        Advanced Optional 1</a>\n",
    "      </h4>\n",
    "    </div>\n",
    "    <div id=\"collapse1-31\" class=\"panel-collapse collapse\">\n",
    "      <div class=\"panel-body\">Create an emply instance of the <i>ALS</i> class and run the <i>explainParams</i> method on it to see the default values.</div>\n",
    "    </div>\n",
    "  </div>\n",
    "  <div class=\"panel panel-default\">\n",
    "    <div class=\"panel-heading\">\n",
    "      <h4 class=\"panel-title\">\n",
    "        <a data-toggle=\"collapse\" data-parent=\"#accordion-31\" href=\"#collapse2-31\">\n",
    "        Hint 1</a>\n",
    "      </h4>\n",
    "    </div>\n",
    "    <div id=\"collapse2-31\" class=\"panel-collapse collapse\">\n",
    "      <div class=\"panel-body\">als1 = ALS(rank=15, maxIter=5, userCol=\"custId\", itemCol=\"stockCode\", ratingCol=\"purch\")</div>\n",
    "    </div>\n",
    "  </div>\n",
    "  <div class=\"panel panel-default\">\n",
    "    <div class=\"panel-heading\">\n",
    "      <h4 class=\"panel-title\">\n",
    "        <a data-toggle=\"collapse\" data-parent=\"#accordion-31\" href=\"#collapse3-31\">\n",
    "        Hint 2</a>\n",
    "      </h4>\n",
    "    </div>\n",
    "    <div id=\"collapse3-31\" class=\"panel-collapse collapse\">\n",
    "      <div class=\"panel-body\">model1 = als1.fit(trainDf)</div>\n",
    "    </div>\n",
    "  </div>\n",
    "  <div class=\"panel panel-default\">\n",
    "    <div class=\"panel-heading\">\n",
    "      <h4 class=\"panel-title\">\n",
    "        <a data-toggle=\"collapse\" data-parent=\"#accordion-31\" href=\"#collapse4-31\">\n",
    "        Hint 3</a>\n",
    "      </h4>\n",
    "    </div>\n",
    "    <div id=\"collapse4-31\" class=\"panel-collapse collapse\">\n",
    "      <div class=\"panel-body\">Type:\n",
    "<br>\n",
    "from pyspark.ml.recommendation import ALS<br>\n",
    "\n",
    "als1 = ALS(rank=15, maxIter=5, userCol=\"custId\", itemCol=\"stockCode\", ratingCol=\"purch\")<br>\n",
    "model1 = als1.fit(trainDf)<br>\n",
    "\n",
    "als2 = ALS(rank=2, maxIter=10, userCol=\"custId\", itemCol=\"stockCode\", ratingCol=\"purch\")<br>\n",
    "model2 = als2.fit(trainDf)\n",
    "</div>\n",
    "    </div>\n",
    "  </div>\n",
    "</div> \n"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 8,
   "metadata": {
    "collapsed": false,
    "scrolled": true
   },
   "outputs": [
    {
     "data": {
      "text/plain": [
       "\"alpha: alpha for implicit preference (default: 1.0)\\ncheckpointInterval: set checkpoint interval (>= 1) or disable checkpoint (-1). E.g. 10 means that the cache will get checkpointed every 10 iterations. (default: 10)\\nfinalStorageLevel: StorageLevel for ALS model factors. (default: MEMORY_AND_DISK)\\nimplicitPrefs: whether to use implicit preference (default: False)\\nintermediateStorageLevel: StorageLevel for intermediate datasets. Cannot be 'NONE'. (default: MEMORY_AND_DISK)\\nitemCol: column name for item ids. Ids must be within the integer value range. (default: item)\\nmaxIter: max number of iterations (>= 0). (default: 10)\\nnonnegative: whether to use nonnegative constraint for least squares (default: False)\\nnumItemBlocks: number of item blocks (default: 10)\\nnumUserBlocks: number of user blocks (default: 10)\\npredictionCol: prediction column name. (default: prediction)\\nrank: rank of the factorization (default: 10)\\nratingCol: column name for ratings (default: rating)\\nregParam: regularization parameter (>= 0). (default: 0.1)\\nseed: random seed. (default: 593367982098446717)\\nuserCol: column name for user ids. Ids must be within the integer value range. (default: user)\""
      ]
     },
     "execution_count": 8,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "from pyspark.ml.recommendation import ALS\n",
    "\n",
    "als1 = ALS(rank=15, maxIter=5, userCol=\"custId\", itemCol=\"stockCode\", ratingCol=\"purch\")\n",
    "model1 = als1.fit(trainDf)\n",
    "\n",
    "als2 = ALS(rank=2, maxIter=10, userCol=\"custId\", itemCol=\"stockCode\", ratingCol=\"purch\")\n",
    "model2 = als2.fit(trainDf)\n",
    "als3 = ALS()\n",
    "als3.explainParams()"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "## Step 4 - Test the models\n",
    "\n",
    "Use the models to predict what the user will rate a certain item.  The closer our model is to 1 for an item a user has already purchased, the better.\n",
    "\n",
    "### 4.1 - Evaluate the model with the cross validation dataframe by using the transorm function.\n",
    "\n",
    "Some of the users or purchases in the cross validation data may not have been in the training data.  Let's remove the ones that aren't.   To do this obtain all the the custId and stockCode values from the training data and filter out any lines with those values from the cross-validation data.\n",
    "<br><br>\n",
    "At the end, print out how many cross-validation lines we had at the start -- and the new number afterwords.\n",
    "<br><br>\n",
    " <div class=\"panel-group\" id=\"accordion-41\">\n",
    "  <div class=\"panel panel-default\">\n",
    "    <div class=\"panel-heading\">\n",
    "      <h4 class=\"panel-title\">\n",
    "        <a data-toggle=\"collapse\" data-parent=\"#accordion-41\" href=\"#collapse1-41\">\n",
    "        Hint 1</a>\n",
    "      </h4>\n",
    "    </div>\n",
    "    <div id=\"collapse1-41\" class=\"panel-collapse collapse\">\n",
    "      <div class=\"panel-body\">Use <i>map()</i> to return a specific value (i.e. foo = foo.map(lambda x: x.value)) and put them all in a set (i.e. foo1 = set(foo))<br></div>\n",
    "    </div>\n",
    "  </div>\n",
    "  <div class=\"panel panel-default\">\n",
    "    <div class=\"panel-heading\">\n",
    "      <h4 class=\"panel-title\">\n",
    "        <a data-toggle=\"collapse\" data-parent=\"#accordion-41\" href=\"#collapse2-41\">\n",
    "        Hint 2</a>\n",
    "      </h4>\n",
    "    </div>\n",
    "    <div id=\"collapse2-41\" class=\"panel-collapse collapse\">\n",
    "      <div class=\"panel-body\">You need all the returned values (remember they might be spread all across the cluster!) so run collect() on the results of the map(). (i.e. foo1 = set(foo.collect()))</div>\n",
    "    </div>\n",
    "  </div>\n",
    "  <div class=\"panel panel-default\">\n",
    "    <div class=\"panel-heading\">\n",
    "      <h4 class=\"panel-title\">\n",
    "        <a data-toggle=\"collapse\" data-parent=\"#accordion-41\" href=\"#collapse3-41\">\n",
    "        Hint 3</a>\n",
    "      </h4>\n",
    "    </div>\n",
    "    <div id=\"collapse3-41\" class=\"panel-collapse collapse\">\n",
    "      <div class=\"panel-body\">Use the <i>filter()</i> to filter out any values in the cross-validation dataframe which are in the stockCode or custId sets.   Use <i>toDF()</i> to change the results to a dataframe.</div>\n",
    "    </div>\n",
    "  </div>\n",
    "  <div class=\"panel panel-default\">\n",
    "    <div class=\"panel-heading\">\n",
    "      <h4 class=\"panel-title\">\n",
    "        <a data-toggle=\"collapse\" data-parent=\"#accordion-41\" href=\"#collapse4-41\">\n",
    "        Hint 4</a>\n",
    "      </h4>\n",
    "    </div>\n",
    "    <div id=\"collapse4-41\" class=\"panel-collapse collapse\">\n",
    "      <div class=\"panel-body\">Type:<br>\n",
    "customers = set(trainDf.rdd.map(lambda line: line.custId).collect())<br>\n",
    "stock = set(trainDf.rdd.map(lambda line: line.stockCode).collect())<br>\n",
    "\n",
    "filteredCvDf = cvDf.rdd.filter(lambda line: line.stockCode in stock and line.custId in customers).toDF()<br>\n",
    "\n",
    "print cvDf.count()<br>\n",
    "print filteredCvDf.count()<br></div>\n",
    "    </div>\n",
    "  </div>\n",
    "</div> "
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 9,
   "metadata": {
    "collapsed": false,
    "scrolled": true
   },
   "outputs": [
    {
     "name": "stdout",
     "output_type": "stream",
     "text": [
      "26330\n",
      "26310\n"
     ]
    }
   ],
   "source": [
    "customers = set(trainDf.rdd.map(lambda line: line.custId).collect())\n",
    "stock = set(trainDf.rdd.map(lambda line: line.stockCode).collect())\n",
    "\n",
    "filteredCvDf = cvDf.rdd.filter(lambda line: line.stockCode in stock and line.custId in customers).toDF()\n",
    "\n",
    "print cvDf.count()\n",
    "print filteredCvDf.count()"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "### Step 4.2 - Make Predictions using <i><a href=\"https://spark.apache.org/docs/1.6.1/api/python/pyspark.ml.html#pyspark.ml.recommendation.ALSModel.transform\">transform()</a></i>\n",
    "\n",
    "Type:\n",
    "\n",
    "predictions1 = model1.transform(filteredCvDf)<br>\n",
    "predictions2 = model2.transform(filteredCvDf)\n",
    "</font>"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 10,
   "metadata": {
    "collapsed": false,
    "scrolled": false
   },
   "outputs": [],
   "source": [
    "predictions1 = model1.transform(filteredCvDf)\n",
    "predictions2 = model2.transform(filteredCvDf)"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "### 4.3 - Calculate and print the Mean Squared Error.   For all ratings, subtract the prediction from the actual purchase (1), square the result, and take the mean of all of the squared differences.\n",
    "\n",
    "The lower the result number, the better the model.\n",
    "\n",
    "Type:\n",
    "\n",
    "meanSquaredError1 = predictions1.rdd.map(lambda line: (line.purch - line.prediction)\\*\\*2).mean()<br>\n",
    "meanSquaredError2 = predictions2.rdd.map(lambda line: (line.purch - line.prediction)\\*\\*2).mean()<br><br>\n",
    "    \n",
    "print 'Mean squared error = %.4f for our first model' % meanSquaredError1<br>\n",
    "print 'Mean squared error = %.4f for our second model' % meanSquaredError2\n"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 11,
   "metadata": {
    "collapsed": false
   },
   "outputs": [
    {
     "name": "stdout",
     "output_type": "stream",
     "text": [
      "Mean squared error = 0.0102 for our first model\n",
      "Mean squared error = 0.0097 for our second model\n"
     ]
    }
   ],
   "source": [
    "meanSquaredError1 = predictions1.rdd.map(lambda line: (line.purch - line.prediction)**2).mean()\n",
    "meanSquaredError2 = predictions2.rdd.map(lambda line: (line.purch - line.prediction)**2).mean()\n",
    "\n",
    "print 'Mean squared error = %.4f for our first model' % meanSquaredError1\n",
    "print 'Mean squared error = %.4f for our second model' % meanSquaredError2"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "### 4.4 - Confirm the model by testing it with the test data and the best hyperparameters found during cross-validation\n",
    "\n",
    "Filter the test dataframe (testDf) the same way as the cross-validation dataframe.   Then run the transform() and calculate the mean squared error.   It should be the same as the value calcuated above.\n",
    "\n",
    "Type:\n",
    "\n",
    "filteredTestDf = testDf.rdd.filter(lambda line: line.stockCode in stock and line.custId in customers).toDF()<br>\n",
    "predictions3 = model2.transform(filteredTestDf)<br>\n",
    "meanSquaredError3 = predictions3.map(lambda line: (line.purch - line.prediction)\\*\\*2).mean()<br><br>\n",
    "    \n",
    "print 'Mean squared error = %.4f for our best model' % meanSquaredError3\n"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 12,
   "metadata": {
    "collapsed": false
   },
   "outputs": [
    {
     "name": "stdout",
     "output_type": "stream",
     "text": [
      "Mean squared error = 0.0097 for our best model\n"
     ]
    }
   ],
   "source": [
    "filteredTestDf = testDf.rdd.filter(lambda line: line.stockCode in stock and line.custId in customers).toDF()\n",
    "predictions3 = model2.transform(filteredTestDf)\n",
    "meanSquaredError3 = predictions3.rdd.map(lambda line: (line.purch - line.prediction)**2).mean()\n",
    "\n",
    "print 'Mean squared error = %.4f for our best model' % meanSquaredError3"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "## Step 5 - Implement the model\n",
    "\n",
    "### 5.1 - First, create a dataframe in which each row has the user id and an item id.\n",
    "<br>\n",
    "Use the <i><a href=\"https://spark.apache.org/docs/1.6.2/api/python/pyspark.sql.html#pyspark.sql.DataFrame\">Dataframe</a></i> methods to create a Dataframe with a specific user and that user's purchased products.<br>\n",
    "&nbsp;&nbsp;&nbsp;&nbsp;First, use the Dataframe <i><a href=\"https://spark.apache.org/docs/1.6.2/api/python/pyspark.sql.html#pyspark.sql.DataFrame.filter\">filter()</a></i> to filter out all custId's but 15544.<br>\n",
    "&nbsp;&nbsp;&nbsp;&nbsp;Then use the <i><a href=\"https://spark.apache.org/docs/1.6.2/api/python/pyspark.sql.html#pyspark.sql.DataFrame.select\">select()</a></i> to only return the <i>custId</i> column.<br>\n",
    "&nbsp;&nbsp;&nbsp;&nbsp;Now use <i><a href=\"https://spark.apache.org/docs/1.6.2/api/python/pyspark.sql.html#pyspark.sql.DataFrame.distinct\">distinct()</a></i> to ensure we only have the single custId.<br>\n",
    "&nbsp;&nbsp;&nbsp;&nbsp;Do a <i><a href=\"https://spark.apache.org/docs/1.6.2/api/python/pyspark.sql.html#pyspark.sql.DataFrame.join\">join()</a></i> with the distinct values from the stockCode column.\n",
    "<br><br>\n",
    " <div class=\"panel-group\" id=\"accordion-51\">\n",
    "  <div class=\"panel panel-default\">\n",
    "    <div class=\"panel-heading\">\n",
    "      <h4 class=\"panel-title\">\n",
    "        <a data-toggle=\"collapse\" data-parent=\"#accordion-51\" href=\"#collapse1-51\">\n",
    "        Hint 1</a>\n",
    "      </h4>\n",
    "    </div>\n",
    "    <div id=\"collapse1-51\" class=\"panel-collapse collapse\">\n",
    "      <div class=\"panel-body\">Use the Dataframe <i>filter()</i> method to filter out all users but 15544<br>\n",
    "      user = trainDf.filter(trainDf.custId == 15544)<br></div>\n",
    "    </div>\n",
    "  </div>\n",
    "  <div class=\"panel panel-default\">\n",
    "    <div class=\"panel-heading\">\n",
    "      <h4 class=\"panel-title\">\n",
    "        <a data-toggle=\"collapse\" data-parent=\"#accordion-51\" href=\"#collapse2-51\">\n",
    "        Hint 2</a>\n",
    "      </h4>\n",
    "    </div>\n",
    "    <div id=\"collapse2-51\" class=\"panel-collapse collapse\">\n",
    "      <div class=\"panel-body\">Use the Dataframe <i>select()</i> method to only select the custId column<br>\n",
    "      userCustId = user.select(\"custId\")</div>\n",
    "    </div>\n",
    "  </div>\n",
    "  <div class=\"panel panel-default\">\n",
    "    <div class=\"panel-heading\">\n",
    "      <h4 class=\"panel-title\">\n",
    "        <a data-toggle=\"collapse\" data-parent=\"#accordion-51\" href=\"#collapse3-51\">\n",
    "        Hint 3</a>\n",
    "      </h4>\n",
    "    </div>\n",
    "    <div id=\"collapse3-51\" class=\"panel-collapse collapse\">\n",
    "      <div class=\"panel-body\">Use the Dataframe <i>distinct()</i> method to only return unique rows.<br>\n",
    "      userCustIdDistinct = userCustId.distinct()</div>\n",
    "    </div>\n",
    "  </div>\n",
    "  <div class=\"panel panel-default\">\n",
    "    <div class=\"panel-heading\">\n",
    "      <h4 class=\"panel-title\">\n",
    "        <a data-toggle=\"collapse\" data-parent=\"#accordion-51\" href=\"#collapse4-51\">\n",
    "        Hint 4</a>\n",
    "      </h4>\n",
    "    </div>\n",
    "    <div id=\"collapse4-51\" class=\"panel-collapse collapse\">\n",
    "      <div class=\"panel-body\">Use the Dataframe <i>join()</i> method to join the results with distinct stockCodes</div>\n",
    "    </div>\n",
    "  </div>\n",
    "    <div class=\"panel panel-default\">\n",
    "    <div class=\"panel-heading\">\n",
    "      <h4 class=\"panel-title\">\n",
    "        <a data-toggle=\"collapse\" data-parent=\"#accordion-51\" href=\"#collapse4-51\">\n",
    "        Hint 5</a>\n",
    "      </h4>\n",
    "    </div>\n",
    "    <div id=\"collapse5-51\" class=\"panel-collapse collapse\">\n",
    "      <div class=\"panel-body\">Type:<br>\n",
    "user = trainDf.filter(trainDf.custId == 15544)<br>\n",
    "userCustId = user.select(\"custId\")<br>\n",
    "userCustIdDistinct = userCustId.distinct()<br>\n",
    "stockCode = trainDf.select(\"stockCode\")<br>\n",
    "stockCodeDistinct = stockCode.distinct()<br>\n",
    "userItems = userCustIdDistinct.join(stockCodeDistinct)<br>\n",
    "OR\n",
    "userItems = trainDf.filter(trainDf.custId == 15544).select(\"custId\").distinct().join( trainDf.select(\"stockCode\").distinct())<br></div>\n",
    "    </div>\n",
    "  </div>\n",
    "</div> "
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 13,
   "metadata": {
    "collapsed": false,
    "scrolled": true
   },
   "outputs": [
    {
     "data": {
      "text/plain": [
       "Row(custId=15544, stockCode=22429)"
      ]
     },
     "execution_count": 13,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "#We will need to configure spark to let us do a cartesian join\n",
    "spark.conf.set(\"spark.sql.crossJoin.enabled\", True)\n",
    "\n",
    "userItems = trainDf.filter(trainDf.custId == 15544).select(\"custId\").distinct().join( trainDf.select(\"stockCode\").distinct())\n",
    "#user = trainDf.filter(trainDf.custId == 15544)\n",
    "#userCustId = user.select(\"custId\")\n",
    "#userCustIdDistinct = userCustId.distinct()\n",
    "#stockCode = trainDf.select(\"stockCode\")\n",
    "#stockCodeDistinct = stockCode.distinct()\n",
    "#userItems = userCustIdDistinct.join(stockCodeDistinct)\n",
    "\n",
    "\n",
    "\n"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "### 5.2 - Use 'transform' to rate each item.\n",
    "\n",
    "Type:\n",
    "\n",
    "bestRecsDf = model2.transform(userItems)<br>\n",
    "bestRecsDf.first()\n"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 14,
   "metadata": {
    "collapsed": false,
    "scrolled": true
   },
   "outputs": [
    {
     "data": {
      "text/plain": [
       "Row(custId=15544, stockCode=20735, prediction=0.9013764262199402)"
      ]
     },
     "execution_count": 14,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "bestRecsDf = model2.transform(userItems)\n",
    "bestRecsDf.first()                                                                                                                      "
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "###  5.3 - Print the top 5 recommendations sorted on prediction.\n",
    "\n",
    " <div class=\"panel-group\" id=\"accordion-53\">\n",
    "  <div class=\"panel panel-default\">\n",
    "    <div class=\"panel-heading\">\n",
    "      <h4 class=\"panel-title\">\n",
    "        <a data-toggle=\"collapse\" data-parent=\"#accordion-53\" href=\"#collapse1-53\">\n",
    "        Hint 1</a>\n",
    "      </h4>\n",
    "    </div>\n",
    "    <div id=\"collapse1-53\" class=\"panel-collapse collapse\">\n",
    "      <div class=\"panel-body\">In order to print the top five recommendations, we need to <i><a href\"https://spark.apache.org/docs/1.6.2/api/python/pyspark.sql.html#pyspark.sql.DataFrame.sort\">sort()</a></i> them in descending order<br></div>\n",
    "    </div>\n",
    "  </div>\n",
    "  <div class=\"panel panel-default\">\n",
    "    <div class=\"panel-heading\">\n",
    "      <h4 class=\"panel-title\">\n",
    "        <a data-toggle=\"collapse\" data-parent=\"#accordion-53\" href=\"#collapse2-53\">\n",
    "        Hint 2</a>\n",
    "      </h4>\n",
    "    </div>\n",
    "    <div id=\"collapse2-53\" class=\"panel-collapse collapse\">\n",
    "      <div class=\"panel-body\">Use <i>take()</i> to get the top 5 values.</div>\n",
    "    </div>\n",
    "  </div>\n",
    "  <div class=\"panel panel-default\">\n",
    "    <div class=\"panel-heading\">\n",
    "      <h4 class=\"panel-title\">\n",
    "        <a data-toggle=\"collapse\" data-parent=\"#accordion-53\" href=\"#collapse3-53\">\n",
    "        Hint 3</a>\n",
    "      </h4>\n",
    "    </div>\n",
    "    <div id=\"collapse3-53\" class=\"panel-collapse collapse\">\n",
    "      <div class=\"panel-body\">Type:<br>\n",
    "      print bestRecsDf.sort(\"prediction\",ascending=False).take(5)</div>\n",
    "    </div>\n",
    "  </div>\n",
    "  <div class=\"panel panel-default\">\n",
    "    <div class=\"panel-heading\">\n",
    "      <h4 class=\"panel-title\">\n",
    "        <a data-toggle=\"collapse\" data-parent=\"#accordion-53\" href=\"#collapse4-53\">\n",
    "        Advanced Optional 1</a>\n",
    "      </h4>\n",
    "    </div>\n",
    "    <div id=\"collapse4-53\" class=\"panel-collapse collapse\">\n",
    "      <div class=\"panel-body\">select &#42; from the retailPurchases temp table on stockCode to see some of selections recommended.</div>\n",
    "    </div>\n",
    "  </div>\n",
    "</div> "
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 15,
   "metadata": {
    "collapsed": false,
    "scrolled": true
   },
   "outputs": [
    {
     "name": "stdout",
     "output_type": "stream",
     "text": [
      "[Row(custId=15544, stockCode=90012, prediction=0.9013963937759399), Row(custId=15544, stockCode=90000, prediction=0.9013766050338745), Row(custId=15544, stockCode=20719, prediction=0.901376485824585), Row(custId=15544, stockCode=23439, prediction=0.901376485824585), Row(custId=15544, stockCode=23284, prediction=0.901376485824585)]\n"
     ]
    },
    {
     "data": {
      "text/html": [
       "<div>\n",
       "<table border=\"1\" class=\"dataframe\">\n",
       "  <thead>\n",
       "    <tr style=\"text-align: right;\">\n",
       "      <th></th>\n",
       "      <th>country</th>\n",
       "      <th>custId</th>\n",
       "      <th>description</th>\n",
       "      <th>inv</th>\n",
       "      <th>invDate</th>\n",
       "      <th>price</th>\n",
       "      <th>quant</th>\n",
       "      <th>stockCode</th>\n",
       "    </tr>\n",
       "  </thead>\n",
       "  <tbody>\n",
       "    <tr>\n",
       "      <th>0</th>\n",
       "      <td>United Kingdom</td>\n",
       "      <td>15361</td>\n",
       "      <td>BLACK CHRISTMAS FLOCK DROPLET</td>\n",
       "      <td>538527</td>\n",
       "      <td>12/13/10 9:52</td>\n",
       "      <td>1.25</td>\n",
       "      <td>24</td>\n",
       "      <td>35610</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>1</th>\n",
       "      <td>United Kingdom</td>\n",
       "      <td>15361</td>\n",
       "      <td>WHITE CHRISTMAS FLOCK DROPLET</td>\n",
       "      <td>538527</td>\n",
       "      <td>12/13/10 9:52</td>\n",
       "      <td>1.25</td>\n",
       "      <td>24</td>\n",
       "      <td>35610</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>2</th>\n",
       "      <td>United Kingdom</td>\n",
       "      <td>15512</td>\n",
       "      <td>PINK CHRISTMAS FLOCK DROPLET</td>\n",
       "      <td>538993</td>\n",
       "      <td>12/15/10 12:01</td>\n",
       "      <td>1.25</td>\n",
       "      <td>8</td>\n",
       "      <td>35610</td>\n",
       "    </tr>\n",
       "  </tbody>\n",
       "</table>\n",
       "</div>"
      ],
      "text/plain": [
       "          country  custId                     description     inv  \\\n",
       "0  United Kingdom   15361  BLACK CHRISTMAS FLOCK DROPLET   538527   \n",
       "1  United Kingdom   15361  WHITE CHRISTMAS FLOCK DROPLET   538527   \n",
       "2  United Kingdom   15512   PINK CHRISTMAS FLOCK DROPLET   538993   \n",
       "\n",
       "          invDate  price  quant  stockCode  \n",
       "0   12/13/10 9:52   1.25     24      35610  \n",
       "1   12/13/10 9:52   1.25     24      35610  \n",
       "2  12/15/10 12:01   1.25      8      35610  "
      ]
     },
     "execution_count": 15,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "print bestRecsDf.sort(\"prediction\",ascending=False).take(5)\n",
    "values = spark.sql(\"select * from retailPurchases where stockCode='35610'\")\n",
    "values.toPandas()"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "Let's look up this user and the recommended product ID's in the excel file...\n",
    "\n",
    "<img src='https://raw.githubusercontent.com/rosswlewis/RecommendationPoT/master/user.png' width=\"80%\" height=\"80%\"></img>"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {
    "collapsed": true
   },
   "source": [
    "This user seems to have purchased a lot of childrens gifts and some holiday items.  The recommendation engine we created suggested some items along these lines\n"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "#####  Citation\n",
    "Daqing Chen, Sai Liang Sain, and Kun Guo, Data mining for the online retail industry: A case study of RFM model-based customer segmentation using data mining, Journal of Database Marketing and Customer Strategy Management, Vol. 19, No. 3, pp. 197â€“208, 2012 (Published online before print: 27 August 2012. doi: 10.1057/dbm.2012.17)."
   ]
  }
 ],
 "metadata": {
  "kernelspec": {
   "display_name": "Python 2 with Spark 2.0",
   "language": "python",
   "name": "python2-spark20"
  },
  "language_info": {
   "codemirror_mode": {
    "name": "ipython",
    "version": 2
   },
   "file_extension": ".py",
   "mimetype": "text/x-python",
   "name": "python",
   "nbconvert_exporter": "python",
   "pygments_lexer": "ipython2",
   "version": "2.7.11"
  }
 },
 "nbformat": 4,
 "nbformat_minor": 0
}
