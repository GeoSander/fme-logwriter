# FME® LogWriter

## About
Logs user-defined messages to FME's log file, optionally preceded and/or followed by a line divider. If desired, the _LogWriter_ can output a log feature that contains the following attributes:

_\_logwriter.level_  
_\_logwriter.message_  
_\_logwriter.time_  

Log features will be created if _Create Log Features_ is set to anything else than _No_. You can use these features to write/push the (formatted) message to another file, a database or some web API for example. You can also use it in combination with a [Terminator](https://www.safe.com/transformers/terminator/) or it could serve as some kind of trigger feature within your workspace. The _Write Log Message_ parameter influences when these features will be output.

### Notes  
- Also available on [FME Hub](https://hub.safe.com/transformers/logwriter) for convenient installation.  
- This transformer has been tested on Python 2.7 and 3.4.  
- Released under [GNU General Public License v3.0](https://github.com/SanderSchaminee/fme-logwriter/blob/master/LICENSE).  
- If you notice a bug or desire a new feature, please contact me. Or make a pull request!  
- The [test workspace](https://github.com/SanderSchaminee/fme-logwriter/blob/master/LogWriterTest.fmw) is used for testing and provides some examples.

## Usage
**Write Log Message**  
Determines when the message will be logged. You can log right before each feature, or only before the first or directly after the last one that passes through the transformer. The latter is a nice option in case you want to print some kind of summary, for instance.  
Note that this setting also influences the _Create Log Features_ parameter, since log features will be created at the same time as the log message is written, but it will _not_ influence the amount of features leaving the _Output_ port: that should always be equal to the amount of input features.

**Message Level**  
Specifies the "severity level" of the message you want to log. In FME Workbench, warnings will be logged in blue, (fatal) errors in red and all other types in black. Also, the message will be prefixed with the level accordingly (e.g. WARN, ERROR etc.), but this will only show up in the actual log file and not in FME's Translation Log window.

**Create Log Features**  
When set to _No_ (default), the _LogMessages_ port will not be used. When set to _Each Message_, a feature will be created for each feature that was logged. Note that this setting depends on the _Write Log Message_ setting, e.g. if _After Last Feature_ was specified there, only 1 log feature will be output right after the last feature left the transformer.  
The log feature stores the message level, text and time, similar to the [LogMessageStreamer](https://www.safe.com/transformers/log-message-streamer/). See the overview section of this documentation for details.  
When set to _Each Message incl. Line(s)_, the message will include the _Preceding Line_ and/or _Succeeding Line_ set below.

**Preceding Line**  
If desired, the message can be preceded by a blank/white line or a line divider (similar to FME's line style).  
A line will be 75 characters long, which is the same length as FME's [Logger](https://www.safe.com/transformers/logger/) uses, but 3 characters shorter than the line dividers FME prints at the end of the translation.

**Log Message(s)**  
Specify the (multiline) text you want to log. You can type a static message, create a dynamic message using attribute values and workspace parameters or directly pass in the value of an attribute. Note that if your message consists of multiple lines, it will be split into separate lines in the log file.

**Succeeding Line**  
If desired, the message can be succeeded by a blank/white line or line divider. See _Preceding Line_.