# Smart Chicken Coop

**EEE174/CpE185 Project** 

**Team Name: Coop-a-Cabana**   
                      



##Introduction
The project will be a chicken coop that uses sensors and communication systems to make it
easy for someone who has limited time or experience to be able to house chickens safely. The
sensors will include a temperature sensor that will use controllers to determine the intensity of
heat lamps, a flow sensor that will be placed in conjunction with the automatic waterer to
determine if there is a leak or a clog in the system. The roof will have solar panels that will
charge a battery system to power all of these devices. There will be a weight sensor that when
properly calibrated will inform the user if there is an egg. There will be a smoke detector that will
activate a small sprinkler off of the waterer’s supply if smoke is detected as a fire safety device if
the heat lamps fail. A motor will be used to spin an arm that spreads feed out at specified times.


##Ramandeep Chumber Labs

[Lab 6: Light Sensor (Digital Photo-resistor with Raspberry Pi)](https://bitbucket.org/coopacabana/project/wiki/Lab%206:%20Light%20Sensor%20(Digital%20Photo-resistor%20with%20Raspberry%20Pi)

[Lab 7: Generate Clock Events](https://bitbucket.org/coopacabana/project/wiki/Lab%207:%20Generate%20Clock%20events%20using%20Pi)

[Lab 8: Charging Battery with Solar Panel](https://bitbucket.org/coopacabana/project/wiki/Lab%208:%20Charging%20Battery%20with%20Solar%20Panel)

[Lab 9: Activating Stepper Motor with Raspberry Pi to control door](https://bitbucket.org/coopacabana/project/wiki/Lab%209:%20Activating%20Stepper%20motor%20with%20Raspberry%20Pi%20to%20control%20door)

[Lab 10: Charging Battery with Solar Panel and Raspberry Pi](https://bitbucket.org/coopacabana/project/wiki/Lab%2010:%20Charging%20Battery%20with%20Solar%20Panel%20and%20Raspberry%20Pi)






## Wiki features

This wiki uses the [Markdown](http://daringfireball.net/projects/markdown/) syntax. The [MarkDownDemo tutorial](https://bitbucket.org/tutorials/markdowndemo) shows how various elements are rendered. The [Bitbucket documentation](https://confluence.atlassian.com/x/FA4zDQ) has more information about using a wiki.

The wiki itself is actually a git repository, which means you can clone it, edit it locally/offline, add images or any other file type, and push it back to us. It will be live immediately.

Go ahead and try:

```
$ git clone https://bitbucket.org/coopacabana/project.git/wiki
```

Wiki pages are normal files, with the .md extension. You can edit them locally, as well as creating new ones.

## Syntax highlighting


You can also highlight snippets of text (we use the excellent [Pygments][] library).

[Pygments]: http://pygments.org/


Here's an example of some Python code:

```
#!python

def wiki_rocks(text):
    formatter = lambda t: "funky"+t
    return formatter(text)
```


You can check out the source of this page to see how that's done, and make sure to bookmark [the vast library of Pygment lexers][lexers], we accept the 'short name' or the 'mimetype' of anything in there.
[lexers]: http://pygments.org/docs/lexers/


Have fun!