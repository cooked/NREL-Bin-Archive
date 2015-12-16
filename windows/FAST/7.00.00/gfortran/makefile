# FAST makefile rev 2.00
# Author: 	Stefano Cottafavi 
# Date: 	04/2011 
# Notes:  	(Eclipse + Photran)||(Manual) + free FORTRAN compiler on Windows
#			for FAST 7.00.00		

workspace_loc 	:= C:\DATI\StefanoCottafavi\NREL
MATLAB 			:= C:\Programmi\MATLAB\R2008b

FAST 			:= 7.00.00
AeroDyn 		:= 13.00.00
NWTCLibrary		:= 1.02.00

# Source folders
VPATH := 	$(workspace_loc)-TWE/NWTCLibrary/$(NWTCLibrary)/Source \
			$(workspace_loc)/FAST/$(FAST)/Source \
			$(workspace_loc)/FAST/$(FAST)/Simulink/Source \
			$(workspace_loc)/AeroDyn/$(AeroDyn)/Source \
			$(workspace_loc)/AeroDyn/$(AeroDyn)/Source/InflowWind/Source
			
# Commands
FC 		:= gfortran -g
OPTIONS	:= -O3 -ffree-line-length-0
LDFLAGS := -static-libgcc -static-libgfortran	# otherwise dependent @ runtime on mingw dlls

PR 		:= 	SysGnu.o
PR 		+= 	NWTC_IO.o NWTC_Num.o NWTC_Aero.o NWTC_Library.o \
			SharedInflowDefs.o HHWind.o FFWind.o FDWind.o CTWind.o UserWind.o InflowWindMod.o \
			SharedTypes.o AeroMods.o GenSubs.o AeroSubs.o AeroDyn.o \
			fftpack.o FFTMod.o HydroCalc.o FAST_Mods.o Noise.o \
			FAST_IO.o FAST.o FAST2ADAMS.o FAST_Lin.o
PR_EXE 	:=	PitchCntrl_ACH.o UserSubs.o UserVSCont_KP.o
PR_BLD 	:= 	BladedDLLInterfaceWindowsDLL.o UserSubs_forBladedDLL.o UserVSCont_KP_forBladedDLL.o
PR_END 	:= 	AeroCalc.o SetVersion.o

# Executable
PREREQ_EXE 	:= SingPrec.o $(PR) $(PR_EXE) $(PR_END) FAST_Prog.o 
# Executable with external .dll controller (GH Bladed)
PREREQ_DLL 	:= SingPrec.o $(PR) $(PR_BLD) $(PR_END) FAST_Prog.o
# Simulink S-func
PREREQ_MEX 	:= DoubPrec.o $(PR) $(PR_EXE) $(PR_END) FastSimulink.o FastGateway.o


# PHONY targets
.PHONY : all clean

# Targets
FAST_$(FAST): $(PREREQ_EXE)
	$(FC) $^ $(LDFLAGS) -o $@.exe
FAST_$(FAST)_Bld: $(PREREQ_DLL)
	$(FC) $^ $(LDFLAGS)  -lkernel32 -o $@.exe #-enable-stdcall-fixup
FAST_$(FAST)_SFunc: $(PREREQ_MEX)
	$(FC) $^ $(LDFLAGS) -shared -DMATLAB_MEX_FILE -L$(MATLAB)\bin\win32 -lmex -lmat -lmx -o $@.mex32
	
fftpack.o: %.o: %.f
	${FC} -c -I$(MATLAB)\include ${OPTIONS} $< -o $@
%.o: %.f90
	${FC} -c -I$(MATLAB)\include ${OPTIONS} $< -o $@
HydroCalc.o: HydroCalcGnu.f90
	${FC} -c -I$(MATLAB)\include ${OPTIONS} $< -o $@
	
clean:
	rm -f *.mod *.o
	