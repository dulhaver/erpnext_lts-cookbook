# ERPNEXT LTS cookbook

## Bench
Bench is the entry-point to ERPNext.  It is the first git repository you clone during installation.

Bench is a Python application.  When you download Bench, you are seeing the _packaged_ module: https://packaging.python.org/tutorials/packaging-projects/

So we use **pip** (a package installer), to install the Bench application.  This includes installing required dependencies, which are extremely important when considering a Long Term Support installation.

### setup.py
During a normal installation, the prerequisites for Bench are driven by **setup.py**.  Specifically, 2 parameters:

1. packages = find_packages()
2. install_requires=install_requires

Here's a snippet of what that looks like, inside of setup.py

 ```
 setup(
	name='bench',
	description='Metadata driven, full-stack web framework',
	author='Frappe Technologies',
	author_email='info@frappe.io',
	version=version,
	packages=find_packages(),
	zip_safe=False,
	include_package_data=True,
	install_requires=install_requires,
	entry_points='''
[console_scripts]
bench=bench.cli:cli
'''
)
```
### install_requires 

The "install_requires" are known as Abstract requirements.  They are the _minimum_ requirements for the Python package to install and work correctly.
  * You _do not specify the source_ of the requirements.
  * You _do not specify the version_ of the requirements, unless you **know** a particular version does not work, or is necessary.

During a typical installation, this is sufficient.  But for a stable, Long Term Support installation?  You need to make sure you're using _specific_ requirements.  And that is where "requirements.txt" comes into play.

### Requirements Files
https://pip.pypa.io/en/latest/user_guide/#requirements-files

Requirements files are ideal when you need to make a repeatable installation.  You specify your Requirements Files as a parameter when calling pip.
```
sudo -H pip3.7 install -e bench-repo -r requirements_LTS_v10.txt
```

The requirements files contains specific information, especially version numbers, of all your dependencies.

### TODO
  - Update Bench on Github; add a valid Requirements File for Bench version 4.10 (current as of March 19th 2019)
  - Search through all the Bench code, and make sure packages aren't being installed by other means.
  
## Frappe
