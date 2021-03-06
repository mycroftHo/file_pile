# FilePile

FilePile creates N random files, based on a given size and type profile and containing some random combination of input words. It's intended use is for generating test files for load testing purposes. An example word list (input_files/words.csv), a size profile (input_files/weights.csv) and a type profile (input_files/types.csv) have been included in this repo. 
## Installation
FilePile uses escript to generate an executable. You must have elixir and erlang installed on your machine. 
To generate this executable:

```bash
git clone https://github.com/mycroftHo/file_pile.git
cd file_pile
mix deps.get
mix escript.build
```
    
*NB* This program requires you to have libreoffice installed in order to generate word documents and pdfs.

## Usage
To generate you files run the following command in the same directory where you generated the executable:

```bash
./filepile --n 10 --outdir "outputdirectory"
```
This will generate 10 files in the outputdirectory using input_files/weights.csv, input_files/types.csv and input_files/words.csv as the input word list.
Please note that you should use full paths to files and directories when calling this script.

## Using Your Own Size Profile
The idea of FilePile is to create a number of files that mirror the intended file profile of your system. The size and type profile files in the input_files directory are CSV files with two columns. 
One column represents file size (in bytes) or file type, and the other column is the likelihood of a file of that size or type appearing in your system.
So if you have two rows

| Size     | Weight |
| :-----:      | :-----:       |
| 10000 | 1   |
| 20000     | 2     |

There will be roughly twice as many 20kb files as 10kb files.

The type weights file is roughly similar but instead maps the likelihood of a given file type appearing in the resulting files. Currently file_pile supports the creation of txt, .docx, and .pdf files. 
