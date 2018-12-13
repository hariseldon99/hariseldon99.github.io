****** Useful Free/Open-Source Software: ******
******   ******
** This is a list of free and open source software that I find useful for
academic work. It contains numerical computing libraries, APIs, Integrated
Development Environments, programming languages designed for scientific
computing, and open source alternatives to proprietary tools.   **
** Products highlighted in a blue background like this emphasis are strongly
recommended **
Index:
   1. Numerical_libraries_and_APIs
   2. Data_storage,_analysis_and_visualization_software
   3. Computer_Algebra_Systems
   4. Integrated_Development_Environments
   5. Source_Control/Revision_Control
   6. Tools_for_drawing_Feynman_Diagrams
   7. LaTeX _and_BibTeX_editors
   8. Rendering_math_on_the_web
   9. arXiv_tools
  10. Image_and_Document_Manipulation
  11. PDF_Creation_and_Manipulation
  12. Unix_Pseudoshells_for_Windows
  13. Website_Authoring/Composition
  14. Online_Backup_and_Cloud_Storage
  15. Open_Source_Fonts_for_Presentations_and_Printing
  16. Miscellaneous
 
 ___________________________________________________________________________________________________________________________________________________________________
|Numerical         |                                                          |                                                                           |Supported|
|libraries and     |Name and Link                                             |Description                                                                |Platforms|
|APIs:_____________|__________________________________________________________|___________________________________________________________________________|_________|
|                  |                                                          |A powerful, free, open source and considerably less painful alternative to |         |
|                  |                                                          |Numerical_Recipes or NAG.                                                  |         |
|                  |                                                          |                                                                           |         |
|                  |                                                          |Notes:                                                                     |         |
|                 |GNU_Scientific_Library_(gsl)                              |   1. For those afflicted with fortranitis, a FORTRAN interface to gsl     |,        |
|                  |                                                          |      (tested with gfortran 4.6.3 on x86-64 linux kernel 3.2.0-24 and gsl  |         |
|                  |                                                          |      version_1.15) can befound_here_.                                     |         |
|                  |                                                          |   2. Click_here for C++ bindings to gsl                                   |         |
|                  |                                                          |   3. Click_here for python bindings to gsl                                |         |
|__________________|__________________________________________________________|___4._Can_be_used_in_windows_through_Cygwin_or_MinGW_______________________|_________|
|                  |                                                          |GCC Quad-Precision Math Library API                                        |         |
|                  |                                                          |                                                                           |         |
|                  |                                                          |Note:                                                                      |         |
|                 |libquadmath                                               |In this library, the 128-bit floating point type "__float128" has twice as |,        |
|                  |                                                          |many bits as a double. The quadmath functions have the same name as their  |         |
|                  |                                                          |standard math.h counterparts, but with a q added on the end, such as log10q|         |
|__________________|__________________________________________________________|and_fmodq_below.___________________________________________________________|_________|
|                 |mpmath_for_Python                                         |Python library for real and complex floating-point arithmetic with         |,        |
|__________________|__________________________________________________________|arbitrary_precision________________________________________________________|_________|
|                  |                                                          |Cross-platform software utility library that provides data structures,     |         |
|                  |                                                          |linked lists, hash tables,                                                 |         |
|                  |                                                          |dynamic strings , dynamic arrays, balanced binary trees, N-ary trees,      |         |
|                  |                                                          |quarks, keyed data lists, relations and tuples.                            |         |
|                 |Glib                                                      |                                                                           |,        |
|                  |                                                          |                                                                           |         |
|                  |                                                          |Notes:                                                                     |         |
|                  |                                                          |   1. Can be used in windows throughCygwin                                 |         |
|__________________|__________________________________________________________|___2._ Another_howto_manual_available_here._______________________________|_________|
|                  |Scipy/Matplotlib                                          |Library modules  for the Python_programming_language  that are designed f|r        |
|                 |                                                          |scientific/numerical computing and data plotting/graphics                  |, ,     |
|                  |                                                          |                                                                           |         |
|__________________|Python(x,y) /_Anaconda___________________________________|Scientific_Python_distributions____________________________________________|_________|
| ________________|OpenMPI___________________________________________________|MPI_message_passing_in_parallel_computing_environments_____________________|,________|
|                  |                                                          |Open source implementation of the OpenMP shared_memory parallel_computing  |         |
|                  |                                                          |standard. Can be  used with gcc/gfortran and other compilers. Also see    |         |
|                 |GOMP                                                      |pthreads.                                                                  |,        |
|                  |                                                          |                                                                           |         |
|__________________|__________________________________________________________|Note: Can_be_used_in_windows_throughCygwin_or_MinGW_______________________|_________|
|                  |                                                          |Open Source implementation of BLAS (Basic Linear Algebra Subprograms)      |         |
|                 |Openblas                                                  |routines. Multithreaded support, and also has lapack/lapacke built in!   |,        |
|                  |                                                          |Available for FORTRAN and C/C++  (via cblas) programmers.                |         |
|__________________|__________________________________________________________|Note:_ User_manual_can_be_found here_____________________________________|_________|
|                  |                                                          |Scalable Linear Eigenvalue Problem Computation:                            |         |
|                  |                                                          |Parallel linear algebra and matrix diagonalization using MPI and PetSc, the|         |
|                 |Slepc                                                     |Portable Extensible Toolkit for Scientific Computation, inparallel         | ,       |
|                  |                                                          |computingenvironments. Contains parallel Lapack implementation             |         |
|                  |                                                          |                                                                           |         |
|__________________|__________________________________________________________|Note: _Can_be_used_in_windows_through_Cygwin._____________________________|_________|
|Data storage,     |                                                          |                                                                           |         |
|analysis and      |Name and Link                                             |Description                                                                |Supported|
|visualization     |                                                          |                                                                           |Platforms|
|software:_________|__________________________________________________________|___________________________________________________________________________|_________|
|                  |Heirarchical                                              |HDF5 is a unique technology suite that makes possible the management of    |         |
|                  |Data_Format (HDF),                                        |extremely large and complex                                                |         |
|                 |                                                          |data collections. HDF file viewers are HDFView and ViTables                |, ,      |
|                  |                                                          |                                                                           |         |
|                  |Network                                                   |NetCDF is a more advanced version of HDF.                                  |         |
|__________________|Common_Data_Form_(NetCDF)_________________________________|___________________________________________________________________________|_________|
| ________________|Mayavi____________________________________________________|3D_visualization_of_scientific_data________________________________________|,_,______|
|                  |QtiPlot/                                                  |Open Source clones of Origin                                               |         |
|                 |SciDavis                                                  |                                                                           |, ,      |
|__________________|__________________________________________________________|Note:_Windows_binaries_for_qtiplot_can_be_obtained_here____________________|_________|
|                  |                                                          |Extract data from images of plots                                          |         |
|                 |g3data                                                    |                                                                           |,        |
|__________________|__________________________________________________________|Note: _Can_be_used_in_windows_through_Cygwin._____________________________|_________|
|Computer_Algebra  |Name and Link                                             |Description                                                                |Supported|
|Systems:__________|__________________________________________________________|___________________________________________________________________________|Platforms|
|                  |                                                          |Open Source MATLAB clone                                                   |         |
|                  |                                                          |                                                                           |         |
|                 |GNU_Octave                                                |Notes:                                                                     |, ,      |
|                  |                                                          |Linux GUI can be found_here  (via_backend)                                |         |
|                  |                                                          |Windows GUI can be found_here                                              |         |
|__________________|__________________________________________________________|There_is_an_Online_Octave_service_called_Verbosus ________________________|_________|
| ________________|SciLab____________________________________________________|Powerful_and_versatile_Open_Source_Software_for_Numerical_Computation______|,_,______|
|                  |                                                          |Interactive Python provides a shell for interactive computing using Python |         |
|                  |                                                          |and other languages. Useful python libraries include:                      |         |
|                  |                                                          |   1. scipy -  Scientific Python                                          |         |
|                 |Jupyter/IPython                                           |   2. numpy - Numerical Python                                             |, ,      |
|                  |                                                          |   3. matplotlib - Technical Graphics                                      |         |
|                  |                                                          |   4. sympy - Symbolic computing                                           |         |
|__________________|__________________________________________________________|___5._mpi4py_-_Python_bindings_for_MPI_____________________________________|_________|
|                 |Quantum                                                   |Free Mathematica add-on for Dirac_bra-ket_notation and quantum operator    |, ,      |
|__________________|__________________________________________________________|algebra.___________________________________________________________________|_________|
|                 |SNEG_library                                              |Mathematica package that provides a framework for performing calculations  |, ,      |
|__________________|__________________________________________________________|using_second_quantization._________________________________________________|_________|
|                  |                                                          |Mathematica package  that performs  several standard simplifications and�|         |
|                 |DiracQ                                                    |manipulations with operators that arise in quantum  many body physics. The|, ,      |
|                  |                                                          |set of operators include Fermions, Bosons and spins located on a lattice, |         |
|__________________|__________________________________________________________|and_has_the _flexibility_for_extensions.__________________________________|_________|
|Integrated        |                                                          |                                                                           |Supported|
|Development       |Name and Link                                             |Description                                                                |Platforms|
|Environments:_____|__________________________________________________________|___________________________________________________________________________|_________|
| ________________|Geany  _________________________________________________|Basic Integrated_Development_Environment_using_GTK+ on_Linux_____________|_________|
|                  |Code::Blocks                                              |Integrated_Development_Environment for multiple project types              |         |
|                  |                                                          |                                                                           |         |
|                 |                                                          |For those unfortunate souls suffering from fortranitis                     |, ,      |
|                  |Code::Blocks                                              |Note: Needs external FORTRAN compiler.Several_are_supported.Recommend      |         |
|__________________|for_FORTRAN_______________________________________________|gfortran_via_MinGW.________________________________________________________|_________|
|                 |Programmer's                                              |Windows_Notepad for programmers                                            |         |
|__________________|Notepad___________________________________________________|___________________________________________________________________________|_________|
| ________________|Dev-C++___________________________________________________|C/C++_IDE_for_windows_(runs_with_MinGW_or_Cygwin_based_compilers)__________|_________|
|                 |Spyder                                                    |Integrated_Development_Environment for Python designed with scientific     |,        |
|__________________|__________________________________________________________|computing_in_mind._________________________________________________________|_________|
|Source_Control/   |Name and Link                                             |Description                                                                |Supported|
|Revision_Control:_|__________________________________________________________|___________________________________________________________________________|Platforms|
|                 |Git                                                       |A distributed_vcs that is more modern and decentralized than the older svn.|, ,      |
|__________________|__________________________________________________________|Can_be_used_with_servers_like_GitHub_or_Bitbucket__________________________|_________|
|Tools for drawing |Name and Link                                             |Description                                                                |Supported|
|Feynman_Diagrams:_|__________________________________________________________|___________________________________________________________________________|Platforms|
| ________________|JaxoDraw__________________________________________________|Java_program_for_drawing_Feynman_Diagrams__________________________________|,_,______|
|                 |Inkscape                                                  |Vector_Graphics editor. Can be used to draw Feynman diagrams by_drawing    |, ,      |
|__________________|__________________________________________________________|parametric_curves__________________________________________________________|_________|
|                 |FeynFig                         �|Program for generating Feynman Diagrams in xfig format. Also contains an   |,        |
|__________________|__________________________________________________________|xfig_library_package_containing_Feynman_Diagram_elements.__________________|_________|
|LaTeX  and BibTeX|Name and Link                                             |Description                                                                |Supported|
|editors:__________|__________________________________________________________|___________________________________________________________________________|Platforms|
| ________________|TexStudio_________________________________________________|LaTeX_editor._Cross-platform_______________________________________________|,_,______|
|                 |TeXworks                                                  |Free LaTeX editors                                                         |, ,      |
|__________________|TeXnicCenter______________________________________________|___________________________________________________________________________|_________|
| ________________|JabRef __________________________________________________|BibTeX_editor_written_in_java______________________________________________|,_,______|
|                 |LaTeX-Mk                                                  |Uses GNU_Make to render complex LaTeX docs, simplifying management.        |,        |
|__________________|__________________________________________________________|Note: Can_be_used_in_windows_throughCygwin_or_MinGW_______________________|_________|
|                 |TexMaths                                                  |LaTeX extension for LibreOffice                                            |, ,      |
|__________________|__________________________________________________________|Very_useful_for_embedding_LaTeX_equations_in_presentations_________________|_________|
|Rendering_Math_on |Name and Link                                             |Description                                                                |Supported|
|the_web___________|__________________________________________________________|___________________________________________________________________________|Platforms|
| ________________|MathJax___________________________________________________|Can_render_LaTeX_or_MathML_in_situ_in_the_web_page_itself._Very_handy!_____|,_,______|
| ________________|TeX_for_Gmail_____________________________________________|Can_render_LaTeX_in_Gmail._Super_handy!____________________________________|,_,______|
|                  |LaTeXMathML                                               |                                                                           |         |
|                 |jsMath                                                    |Similar to MathJax above.                                                  |, ,      |
|__________________|ASCIIMathML_______________________________________________|___________________________________________________________________________|_________|
| ________________|LibreOffice_Math__________________________________________|Can_render_math_and_export_it_to_MathML____________________________________|,_,______|
| ________________|TexPaste__________________________________________________|A_pastebin_for_LaTeX.______________________________________________________|,_,______|
|arXiv tools:      |Name and Link                                             |Description                                                                |Supported|
|__________________|__________________________________________________________|___________________________________________________________________________|Platforms|
| ________________|arX_______________________________________________________|iPhone_app_to_access_arXiv_________________________________________________|_________|
|                 |arXiv_mobile                                              |Cellphone app for browsing arXiv                                           |         |
|__________________|for_Android_______________________________________________|___________________________________________________________________________|_________|
|Image and Document|Name and Link                                             |Description                                                                |Supported|
|Manipulation:_____|__________________________________________________________|___________________________________________________________________________|Platforms|
| ________________|ImageMagick_______________________________________________|Powerful_library_for_manipulating/compressing_images_______________________|,_,______|
| ________________|Converseen________________________________________________|Powerful_batch_processing_based_graphical_interface_to_ImageMagick_________|,________|
|                  |                                                          |Toolkit for hacking pdf files                                              |         |
|                  |                                                          |                                                                           |         |
|                 |Pdftk: The PDF toolkit                                    |Notes:                                                                     | ,      |
|                  |                                                          |Linux GUI can be found_here                                                |         |
|__________________|__________________________________________________________|Windows_GUI_can_be_found_here_or_here______________________________________|_________|
|                 |Xournal                                                   |FOSS clone of Windows_Journal. Can be used as a PDF annotator.             |,        |
|__________________|__________________________________________________________|Note:_Windows_client_can_be_found_here_____________________________________|_________|
|                 |PDFescape                                                 |Online tools to annotate PDF documents. Can be used to fill PDF forms.     | ,      |
|__________________|PDF_Buddy_(Freemium)______________________________________|Includessticky_notes!______________________________________________________|_________|
| ________________|pdfedit___________________________________________________|Free_editor_for_PDF_documents______________________________________________|,________|
| ________________|Jpeg2eps__________________________________________________|Script_for_embedding_jpegs_into_eps_containers_using_ghostscript___________|_________|
|PDF Creation and  |Name and Link                                             |Description                                                                |Supported|
|Manipulation:_____|__________________________________________________________|___________________________________________________________________________|Platforms|
| ________________|cups-pdf__________________________________________________|Use_the_print_dialog_to_generate_PDF_files_from_any_application.___________|_________|
| ________________|PDFCreator________________________________________________|Use_the_print_dialog_to_generate_PDF_files_from_any_application.___________|,________|
| ________________|DiffPDF___________________________________________________|DiffPDF_is_used_to_compare_two_PDF_files,_textually_or_visually.___________|,_,______|
| ________________|Filling_PDFforms_inOffice_apps____________________________|Howto_on_filling_PDF_forms_using_OpenOffice/LibreOffice.___________________|,_,______|
|Unix Pseudoshells |Name and Link                                             |Description                                                                |Supported|
|for_Windows:______|__________________________________________________________|___________________________________________________________________________|Platforms|
| ________________|MinGW_____________________________________________________|GNU_shell_environment_for_Windows__________________________________________|_________|
| ________________|Cygwin____________________________________________________|Software_for_imitating_a_Unix_environment_on_Windows_______________________|_________|
|Website_Authoring/|Name and Link                                             |Description                                                                |Supported|
|Composition:______|__________________________________________________________|___________________________________________________________________________|Platforms|
| ________________|Bluegriffon_______________________________________________|WYSIWYG_Web_page_authoring_software________________________________________|,_,______|
| ________________|Notepad, Gedit___________________________________________|Simple_text_editor,_ahem.__________________________________________________|,_,______|
|Online Backup and |Name and Link                                             |Description                                                                |Supported|
|Cloud_Storage:____|__________________________________________________________|___________________________________________________________________________|Platforms|
|                  |                                                          |Sync files and documents with the dropbox server and any desktop, laptop or|, ,      |
|                 |Dropbox                                                   |portable computing device running the dropbox software.                    |,        |
|__________________|__________________________________________________________|___________________________________________________________________________|,________|
|                  |                                                          |Portable_application_conversion_technology. Install compatible apps like   |         |
|                 |PortableApps.com                                          |LibreOffice, Inkscape, Firefox and others into removable_media or cloud    |         |
|__________________|__________________________________________________________|storage._Access_them_on_the_go_from_any_computer.__________________________|_________|
|Open Source Fonts |                                                          |                                                                           |Supported|
|for Presentations |Name and Link                                             |Description                                                                |Platforms|
|and_Printing______|__________________________________________________________|___________________________________________________________________________|_________|
|                  |                                                          |Group typeface font. Looks good when printed.                              |         |
|                 |Bitstream_Vera_Fonts                                      |                                                                           |, ,      |
|                  |                                                          |Note:  LaTeX users can use the Type 1 Postscript version of these fonts   |         |
|__________________|__________________________________________________________|using_the_Bera_package.____________________________________________________|_________|
|                  |                                                          |Mobile-friendly fonts. Originally designed for Android by Google. Download |         |
|                 |Droid_Font_Family                                         |from here.                                                                 |, ,      |
|                  |                                                          |                                                                           |         |
|__________________|__________________________________________________________|Note: _LaTeX_users_can_use _these_fonts_using_the_droid_package._________|_________|
|                 |Liberation_Fonts                                          |Fonts that have metric_compatibility with Microsoft_fonts like Arial, Times|, ,      |
|__________________|__________________________________________________________|New_Roman,_and_Courier_New.________________________________________________|_________|
| ________________|Libertine_Fonts___________________________________________|Open_source_alternative_to_Microsoft's_Times_font_family.__________________|,_,______|
| ________________|Ubuntu_Font_Family________________________________________|The_default_fonts_of_Ubuntu_Linux._________________________________________|,_,______|
| Miscellaneous:   |Name(s) and Link(s)                                       |Description                                                                |Supported|
|__________________|__________________________________________________________|___________________________________________________________________________|Platforms|
|File Transfer:    |WinSCP, Filezilla                                         |Useful tools to transfer files to and from a computer over a network.      |,        |
|__________________|__________________________________________________________|Supports_ftp,_ssh,_scp,_sftp_and_other_protocols___________________________|_________|
|Diff_Viewer:______|Meld______________________________________________________|Visual_diff and_merge_tool_targeted_at_developers_________________________|,________|
|File Archiving and|7-zip, ark                                                |Tools for archiving files and compressing them for transfer over networks, |,        |
|Compression:______|__________________________________________________________|email_attachments,_arXiv_uploads_etc.______________________________________|_________|
|File splitters and|HJSplit, lxSplit                                          |Tools for splitting and recombining large files into and from smaller      |, ,      |
|joiners___________|__________________________________________________________|files._____________________________________________________________________|_________|
| ________________| ________________________________________________________| _________________________________________________________________________| _______|
| ________________|KeepassX__________________________________________________|Create_encrypted_filesystemsfor_sensitive_data_____________________________|,_,______|
| ________________|Calibre___________________________________________________|Powerful_E-book_and_paper_collection_manager_______________________________|,_,______|
| ________________|VimTouch__________________________________________________|Vi/Vim_editor_for_android._Wicked_cool!____________________________________|_________|
|                  |Kalzium                                                   |Periodic_Table_of_Elements with additional tools for atomic/molecular      |         |
|                 |                                                          |physics/chemistry. Linux only                                              |,        |
|                  |                                                          |                                                                           |,        |
|__________________|QPeriodicTable____________________________________________|A_Similar_app_for_Windows_and_Mac__________________________________________|_________|
 
 
[Valid_HTML_4.01_Transitional]
