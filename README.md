# Munki Serial Enroll

A set of scripts to automatically enroll clients in Munki, allowing for a very flexible manifest structure.

## Why Munki Serial Enroll?

Using serial number manifests with human-readable display names and included group manifests allows for maximum flexibility. You can deploy software to a single machine or a group of machines.

### Wait, Doesn't Munki Do This Already?

Munki can target systems based on hostnames or serial numbers. However, each manifest must be created by hand. Munki Serial Enroll allows us to create specific manifests automatically, and to allow them to contain a more generic manifest for large-scale software management.

## How does this differ from regular Munki Enroll?
It has a few logistical tweaks for my organization that others may find immediately helpful or may find ideas in that they can tweak for their own organizations, but it's also different in approach.

The original Munki Enroll creates individual manifests based on hostname and writes the hostname back as a ClientIdentifier on the  client itself. Munki Serial Enroll goes based off of serial number, copies a template manifest (instead of creating one from scratch), and actually deletes the ClientIdentifier entirely.

## Server Configuration

Munki Enroll requires PHP to be working on the webserver hosting your Munki repository.

Copy the **munki-enroll** folder to the root of your Munki repository (the same directory as pkgs, pkginfo, manifests and catalogs). 

Also copy the **desktop_template** and **laptop_template** files to your manifests folder and modify them appropriately. Leave in the
```
	<key>display_name</key>
	<string>DISPLAYNAMETOREPLACE</string>
```
bit, though, because that's what gets replaced later after the template is copied.

Make sure the Apache or other www user has write access to the manifests folder.  

That's it on the server side! Be sure to make note of the full URL path to the enroll.php file.

## Client Configuration

On the client side, tweak (for your organization) the two user-defined variables and run the munki_enroll.sh script, which will then communicate with the server about what manifest to create.

The included munki_enroll.sh script can be executed in any number of ways (Terminal, ARD, DeployStudio workflow, LaunchAgent, etc.).

## Acknowledgements
I've done a lot of work on this, but a lot of credit for this concept must go to [Cody Eding](https://github.com/edingc), the creator of Munki-Enroll, which I forked this from.

## License

Munki-Serial-Enroll is published under the [MIT License](http://www.opensource.org/licenses/mit-license.php).
