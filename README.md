# Example Package

This is a simple example package. You can use
[Github-flavored Markdown](https://guides.github.com/features/mastering-markdown/)
to write your content.

## A simple project

To create this project locally, create the following file structure:

    /packaging_tutorial
      /example_pkg
        __init__.py

Once you create this structure, you’ll want to run all of the commands in this tutorial within the top-level folder - so 
be sure to cd packaging_tutorial.

You should also edit example_pkg/__init__.py and put the following code in there:

    name = "example_pkg"

## Creating the package files

You will now create a handful of files to package up this project and prepare it for distribution. Create the new 
files listed below - you will add content to them in the following steps.

    /packaging_tutorial
      /example_pkg
        __init__.py
      setup.py
      LICENSE
      README.md

### Creating setup.py

setup.py is the build script for setuptools. It tells setuptools about your package (such as the name and version) 
as well as which code files to include.

Open setup.py and enter the following content. You should update the package name to include your username 
(for example, example-pkg-theacodes. 

You can personalize the other values if you’d like:

    import setuptools
    
    with open("README.md", "r") as fh:
        long_description = fh.read()
    
    setuptools.setup(
        name="example-pkg-your-username",
        version="0.0.1",
        author="Example Author",
        author_email="author@example.com",
        description="A small example package",
        long_description=long_description,
        long_description_content_type="text/markdown",
        url="https://github.com/pypa/sampleproject",
        packages=setuptools.find_packages(),
        classifiers=[
            "Programming Language :: Python :: 3",
            "License :: OSI Approved :: MIT License",
            "Operating System :: OS Independent",
        ],
    )


### Creating README.md

Create a README.md and use [Github-flavored Markdown](https://guides.github.com/features/mastering-markdown/). 

### Creating a LICENSE

See [Choose an open source license](https://choosealicense.com/).

## Generating distribution archives

> The next step is to generate distribution packages for the package. These are archives that are uploaded to the 
Package Index and can be installed by pip.

Make sure you have the latest versions of setuptools and wheel installed:

    python -m pip install --user --upgrade setuptools wheel
    python setup.py sdist bdist_wheel
    
This command should output a lot of text and once completed should generate two files in the dist directory:

    dist/
      example_pkg_your_username-0.0.1-py3-none-any.whl
      example_pkg_your_username-0.0.1.tar.gz

The tar.gz file is a source archive whereas the .whl file is a built distribution. Newer pip versions preferentially 
install built distributions, but will fall back to source archives if needed. 

You should always upload a source archive and provide built archives for the platforms your project is compatible with. 
In this case, our example package is compatible with Python on any platform so only one built distribution is needed.

## Uploading the distribution archives

Now that you are registered, you can use twine to upload the distribution packages. You’ll need to install Twine:

    python -m pip install --user --upgrade twine

Once installed, run Twine to upload all of the archives under dist:

    python -m twine upload --repository-url https://test.pypi.org/legacy/ dist/*

Confirm your package is available on `test.pypi.org`.

    https://test.pypi.org/project/example-pkg-russomi/

## Installing your newly uploaded package

You can use pip to install your package and verify that it works. Create a new virtualenv (see Installing Packages 
for detailed instructions) and install your package from TestPyPI:

    python -m pip install --index-url https://test.pypi.org/simple/ example-pkg-russomi

You can test that it was installed correctly by importing the module and referencing the name property you put in __init__.py earlier.

    python
    
    >>> import example_pkg
    >>> example_pkg.name
    'example_pkg'    

Congratulations, you’ve packaged and distributed a Python project! ✨ 🍰 ✨

## Installing the `editable` version of the package for local development

The `pip` way:

    pip install -e /path/to/mypackage
    
The `setuptools` way:

    python /path/to/mypackage/setup.py develop

See [“pip install --editable ./” vs “python setup.py develop”](https://stackoverflow.com/questions/30306099/pip-install-editable-vs-python-setup-py-develop)
for a discussion on differences between the two.

## Reference

* https://test.pypi.org/account/register/
* https://packaging.python.org/tutorials/packaging-projects/
* https://stackoverflow.com/questions/30306099/pip-install-editable-vs-python-setup-py-develop
