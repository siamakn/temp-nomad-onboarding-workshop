
## Preparing a simple local programming environment

To use the NOMAD API, and in general to use NOMAD programmatically, you naturally need a programming environment. While there are several options available, the Python programming language along with some relevant libraries is a good choice among various options. For instance, the `Requests` library enables an HTTP connection to the NOMAD servers. For data analysis and visualization, further libraries will be needed such as 
`NumPy` (a base N-dimensional array package), `SciPy` (a library for scientific computing), and `Matplotlib` (for plotting). An easy way to prepare such programming environment on your computer (local) is to install Python 3 and its most commonly used libraries as a package using Anaconda. Anaconda is a distribution of the Python for scientific computing, that aims to simplify package management and deployment.

To install Anaconda and the required libraries, you can follow these three steps:

1.  Go to the Anaconda download page ([https://www.anaconda.com/download](https://www.anaconda.com/download)) and download the Anaconda installer for Python 3. Follow the steps provided by the installation wizard. If you were unsure about any options, feel free to select the default or recommended choices suggested by the installer. Once the installation is complete, a system reboot might be beneficial. With this step completed, Python 3 and the essential libraries for data analysis and visualization are now ready for use on your system.
    
2.  Open the Anaconda Navigator, which should now be available in your applications or programs list. Launch Jupyter Notebook from the Anaconda Navigator. This will open a new browser window with Jupyter's file explorer. In the Jupyter Notebook interface, click the 'New' button in the top right corner and select 'Python 3' from the drop-down menu. This will create a new Jupyter Notebook with a Python 3 kernel. You may also rename your notebook by clicking on the default title ('Untitled') at the top of the page and entering your desired name. To execute a cell in Jupyter Notebook, press **Shift + Enter**.
    
3. The Requests library, needed for making HTTP requests, is not included in the default Anaconda package. Therefore, it should be installed separately, e.g., using the `pip` package manager. Ensure `pip`  is up-to-date before installing the Requests library. To do this, run the following commands in a Jupyter Notebook cell: 

```python
!pip install --upgrade pip
!pip install requests
```
Please note, you only need to perform the installation steps (1 and 3) once to set up your programming environment for ongoing NOMAD API usage. 



