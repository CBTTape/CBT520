# CBT520
Converted to GitHub via [cbt2git](https://github.com/wizardofzos/cbt2git)

This is still a work in progress. 
Due to amazing work by Alison Zhang and Jake Choi repos are no longer deleted.

```
//***FILE 520 is from Robin Ryerse and contains some REXX           *   FILE 520
//*           functions, written in Assembler.                      *   FILE 520
//*                                                                 *   FILE 520
//*           Their names are:  SCCPDSD, SCCPDSR, and WILDCARD.     *   FILE 520
//*           And a new one is called:   VARLIST                    *   FILE 520
//*                                                                 *   FILE 520
//*     Note: A modification of VARLIST, called VARLISTS, was       *   FILE 520
//*           submitted by Wilfried Eike, which returns the output  *   FILE 520
//*           on the REXX stack so it could be used within a REXX   *   FILE 520
//*           script.                                               *   FILE 520
//*                                                                 *   FILE 520
//*           email:  Wilfried.Eike@t-online.de                     *   FILE 520
//*                                                                 *   FILE 520
//*           Another function has been added to this package,      *   FILE 520
//*           called SCXSORT.  Notes for SCXSORT are found below.   *   FILE 520
//*                                                                 *   FILE 520
//*           Another new function:  SCC@DSN - to determine if      *   FILE 520
//*           a dataset exists.                                     *   FILE 520
//*                                                                 *   FILE 520
//*           A new function package has also been added, called    *   FILE 520
//*           SCCALLOC.  SCCALLOC provides, in native REXX, the     *   FILE 520
//*           functionality of the TSO ALLOCATE and FREE commands,  *   FILE 520
//*           which will now be available to "Address TSO".         *   FILE 520
//*                                                                 *   FILE 520
//*           An additional package, called DSN4DD, tells you,      *   FILE 520
//*           for a dataset in a concatenation, which number of     *   FILE 520
//*           the concatenation that dataset is.                    *   FILE 520
//*                                                                 *   FILE 520
//*           The purpose of these REXX functions is to select      *   FILE 520
//*           certain members of a partitioned dataset, according   *   FILE 520
//*           to some rule, and to allow you to perform, in REXX,   *   FILE 520
//*           some operation on all the members that were           *   FILE 520
//*           selected.                                             *   FILE 520
//*                                                                 *   FILE 520
//*           email:   Robin.Ryerse@stelco.ca                       *   FILE 520
//*                                                                 *   FILE 520
//*           Each package has a $README member with a $ preceding  *   FILE 520
//*           its name.  Each package is actually an unloaded pds   *   FILE 520
//*           in IEBUPDTE SYSIN format (really in PDSLOAD format).  *   FILE 520
//*           The $PDSLOAD member is a job to create a pds out of   *   FILE 520
//*           each member that is really a package.                 *   FILE 520
//*                                                                 *   FILE 520
//*           The member of this file which is called PDSLOAD,      *   FILE 520
//*           is an XMIT-format load library, containing the        *   FILE 520
//*           PDSLOAD load module.  To create the load library,     *   FILE 520
//*           issue the command (under TSO):                        *   FILE 520
//*                                                                 *   FILE 520
//*           RECEIVE INDS(userid.FILE520.PDS(PDSLOAD)),            *   FILE 520
//*                                                                 *   FILE 520
//*           and press ENTER at the prompts.                       *   FILE 520
//*                                                                 *   FILE 520
//*        -  -  -  -  -  -  -  -  -  -  -  -  -  -  -  -  -        *   FILE 520
//*                                                                 *   FILE 520
//*    Special notes for the SCXSORT package:                       *   FILE 520
//*                                                                 *   FILE 520
//*       Name:        SCXSORT                                      *   FILE 520
//*                                                                 *   FILE 520
//*       Purpose:     Sort from and/or into REXX stem              *   FILE 520
//*                    variables.                                   *   FILE 520
//*                                                                 *   FILE 520
//*       Environment: REXX subroutine/function for all MVS/ESA     *   FILE 520
//*                    environments.  SCXSORT resides in the        *   FILE 520
//*                    IRXFLOC "function package".                  *   FILE 520
//*                                                                 *   FILE 520
//*       Features:    All the capabilities of the system sort      *   FILE 520
//*                    program are available.                       *   FILE 520
//*                                                                 *   FILE 520
//*        -  -  -  -  -  -  -  -  -  -  -  -  -  -  -  -  -        *   FILE 520
//*                                                                 *   FILE 520
//*      Installation / readme for SCXSORT                          *   FILE 520
//*                                                                 *   FILE 520
//*      There are 3 components for this package                    *   FILE 520
//*                                                                 *   FILE 520
//*      MACRO    Is the Assembler macro named ID requitred to      *   FILE 520
//*               assemble the assembler routine. Put it into a     *   FILE 520
//*               library included in your SYSLIB concatenation     *   FILE 520
//*               for the assembly.                                 *   FILE 520
//*                                                                 *   FILE 520
//*      SOURCE   Is the single Assembler source deck of the        *   FILE 520
//*               function.                                         *   FILE 520
//*                                                                 *   FILE 520
//*      HELP     Is the documentation on how to use SCXSORT in     *   FILE 520
//*               REXX programs.                                    *   FILE 520
//*                                                                 *   FILE 520
//*      Making SCXSORT available to your REXX program can be as    *   FILE 520
//*      simple as link editing it to a load library that is        *   FILE 520
//*      within the JOBLIB/STEPLIB concatenation when the REXX      *   FILE 520
//*      program runs.  I myself have built a REXX function         *   FILE 520
//*      package under the name IRXFLOC which contains all the      *   FILE 520
//*      assembler written REXX functions for the platform.         *   FILE 520
//*                                                                 *   FILE 520
//*      The HELP documentation should provide all the usage        *   FILE 520
//*      notes required.                                            *   FILE 520
//*                                                                 *   FILE 520
//*        -  -  -  -  -  -  -  -  -  -  -  -  -  -  -  -  -        *   FILE 520
//*                                                                 *   FILE 520
//*    Special notes for the DSN4DD package:                        *   FILE 520
//*                                                                 *   FILE 520
//*    Name:        DSN4DD                                          *   FILE 520
//*                                                                 *   FILE 520
//*    Purpose:     Return the name of (a concatenation level       *   FILE 520
//*                 of) a dataset for a specified DDname.           *   FILE 520
//*                                                                 *   FILE 520
//*    Environment: REXX subroutine/function for all MVS/ESA        *   FILE 520
//*                 environments.  DSN4DD resides in the            *   FILE 520
//*                 IRXFLOC "function package".                     *   FILE 520
//*                                                                 *   FILE 520
//*    Features:    The value of the DSN is returned as per         *   FILE 520
//*                 the invocation construct.                       *   FILE 520
//*                                                                 *   FILE 520
//*                 The REXX variable RC is set to the number       *   FILE 520
//*                 of concatenation levels for the DD.             *   FILE 520
//*                                                                 *   FILE 520
//*    Argument:    The DDname for which the dataset name is        *   FILE 520
//*                 required.                                       *   FILE 520
//*                                                                 *   FILE 520
//*                 The DDname can be further qualified with        *   FILE 520
//*                 a suffix in format  +n  where "n" is a          *   FILE 520
//*                 number relative to 1 of the concatenation       *   FILE 520
//*                 within the DDname.                              *   FILE 520
//*                                                                 *   FILE 520
//*    Results:     DSN4DD operates as a REXX subroutine/function.  *   FILE 520
//*                 When used as a subroutine, the caller           *   FILE 520
//*                 retrieves the value from the REXX variable      *   FILE 520
//*                 RESULT. When used as a function, REXX makes     *   FILE 520
//*                 the requested assignment from the context of    *   FILE 520
//*                 REXX statement which invoked it.                *   FILE 520
//*                                                                 *   FILE 520
//*                 DSN4DD always sets the REXX variable RC.        *   FILE 520
//*                 For a request which is matched without          *   FILE 520
//*                 error, RC is asigned the number of              *   FILE 520
//*                 datasets which are concatenated together.       *   FILE 520
//*                 If there is no concatenation, RC will be        *   FILE 520
//*                 assigned the value one.                         *   FILE 520
//*                                                                 *   FILE 520
//*    Errors/Warnings:                                             *   FILE 520
//*                 If the DDNAME is not allocated or the           *   FILE 520
//*                 argument is missing, RC will be assigned        *   FILE 520
//*                 the value of minus one and the result will      *   FILE 520
//*                 be null.                                        *   FILE 520
//*                                                                 *   FILE 520
//*                 If the DDNAME is allocated but the requested    *   FILE 520
//*                 concatenation level is invalid or beyond the    *   FILE 520
//*                 allocated concatenation level, the 'result'     *   FILE 520
//*                 will be null and RC is assigned the number      *   FILE 520
//*                 of datasets allocated within the                *   FILE 520
//*                 concatenation level.                            *   FILE 520
//*                                                                 *   FILE 520
//*    Notes:       If the DDname is allocated to a member of       *   FILE 520
//*                 a partitioned dataset, the member name is       *   FILE 520
//*                 included in the result. This makes DSN4DD       *   FILE 520
//*                 distinct from the TSO LISTF command.            *   FILE 520
//*                                                                 *   FILE 520
//*        -  -  -  -  -  -  -  -  -  -  -  -  -  -  -  -  -        *   FILE 520
//*                                                                 *   FILE 520
```
