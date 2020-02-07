# MCSimpleConfig
Easily create YAML config files with or without resource, header, and comments. Config files automatically update on disk if resource changes.
___
#### Credits:  
First things first. I want to thank [Log-out](https://bukkit.org/members/log-out.90690580/) for providing the base of this project. And to [kangarko](https://www.spigotmc.org/members/kangarko.3321/) for helping me learn Java and SpigotAPI.

### About this project:
I spent some time scouring the internet looking for help to make such a project before I finally came [this project](https://bukkit.org/threads/tut-custom-yaml-configurations-with-comments.142592/). 
It was designed for use with the [Bukkkit](https://bukkit.org/pages/about-us/) API for [Minecraft](http://www.minecraft.net), or it derivatives such as [Spigot](https://www.spigotmc.org/wiki/about-spigot/) and [Paper](https://papermc.io/). By the time I found it some things had broken. I have tuned it up and brought it back to life, as well as added an auto-update feature. If you try to read a value that is not in the config, but is stored in the resource the config file will automatically update with the default value.

## Features:
Create and manage YAML files with:
* Nicely formatted headers
* Comments added above top-level keys
* Comments that are preserved on save 

##### Example usage:

```java
import org.bukkit.plugin.java.JavaPlugin;
 
public class CLASS_NAME extends JavaPlugin {
 
    public SimpleConfigManager manager;
 
    public SimpleConfig config;
    public SimpleConfig messages;
 
    public void onDisable() {
 
    }
 
    public void onEnable() {
 
        String[] comments = {"Multiple lines", "Of nice comments", "Are supported !"};
        String[] header = {"This is super simple", "And highly customizable", "way to manage YAML files !"};
 
        this.manager = new SimpleConfigManager(this);
 
        this.mainConfig = manager.getNewConfig("config.yml", true, header);
        this.messages = manager.getNewConfig("misc/messages.yml");
 
        this.config.set("path1", "value1", comments);
        this.config.set("path2", "value2", "This is second comment !");
        this.config.saveConfig();
 
    }
 
}
```
Would produce a `config.yml` file in the plugin directory like so:
```yaml
# +----------------------------------------------------+
# <                This is super simple                >
# <              And highly customizable               >
# <            way to manage YAML files !              >
# +----------------------------------------------------+

# Multiple lines
# Of nice comments
# Are supported !
path1: value1

# This is second comment !
path2: value2
```
and a blank `messages.yml` in the `plugin/misc/` directory.


