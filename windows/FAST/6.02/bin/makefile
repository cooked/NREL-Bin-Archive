# FAST 6.02 MEX,EXE - Stefano Cottafavi 07/2008 - Manual makefile
# for Eclipse + Photran + G95 FORTRAN compiler

# Manual (outside Eclipse, so no ConfigName variable has been defined)
ifndef ConfigName
	ConfigName := FAST_6.02
endif
ifndef MATLAB
	MATLAB := C:\Programmi\MATLAB\R2008b\extern
endif

# Source folders
VPATH := 	..\Source \
			..\Source\helpers \
			..\Source\aerodynGNU \
			..\Source\simulink
			
# Commands
FC 		:= gfortran#g95
DEBUG	:= 
OPTIM	:= -O0
INCLUDE :=
WARNING	:= -Wno-line-truncation
OPTIONS	:= -fno-underscoring -ffree-line-length-0 #-fcase-upper #-r8    #(g95)-ffree-line-length-huge 

# Compiler-dependant and common prerequisites
ifeq ($(FC),gfortran)
	PR 	:= SysGfortran.o 
else
	PR 	:= SysG95.o 
endif
PR 		+= fftpack.o FFTMod.o NoiseMods.o FAST_Mods.o AeroSubs.o UserWind.o \
		GenUse.o HydroCalc.o NoiseSubs.o \
		Fast_IO.o Fast.o FAST2ADAMS.o FAST_Lin.o 
PR_EXE 	:=	PitchCntrl_ACH.o UserSubs.o UserVSCont_KP.o
PR_BLD 	:= 	BladedDLLInterfaceGfortran.o UserSubs_forBladedDLL.o UserVSCont_KP_forBladedDLL.o
PR_END  := 	AeroCalc.o SetVersion.o

ifeq ($(ConfigName),FAST_6.02)
	EXT := .exe
	PREREQ := $(PR) AeroMods.o GenSubs.o $(PR_EXE) $(PR_END)Fast_Prog.o
endif
ifeq ($(ConfigName),FAST_6.02_Bld)	# Executable with external .dll GH Bladed control
	EXT 	:= .exe
	LIBRARY	:= -mrtd -enable-stdcall-fixup #-L"C:\MinGW\lib" -lkernel32 -mwindows
	PREREQ 	:= AeroMods.o SysGfortran.o fftpack.o FFTMod.o NoiseMods.o FAST_Mods.o AeroSubs.o UserWind.o \
			GenUse.o HydroCalc.o NoiseSubs.o \
			Fast_IO.o Fast.o FAST2ADAMS.o FAST_Lin.o GenSubs.o kernel32.o FAST_Prog.o
endif
ifeq ($(ConfigName),FAST_6.02s)
	EXT := .dll
	MACRO := -shared -DMATLAB_MEX_FILE
	INCLUDE := -I$(MATLAB)\include
	LIBRARY	:= -L$(MATLAB)\bin\win32 -lmex -lmat -lmx
	PREREQ := $(PR) AeroMods_SFunc.o GenSubs_SFunc.o $(PR_EXE) $(PR_END) FastDynamics.o FastGateway.o
endif 
	 
# PHONY targets
.PHONY : all clean

# PHONY targets
.PHONY : all clean

# Targets
$(ConfigName)$(EXT): $(PREREQ)
		$(FC) $^ $(MACRO) $(LIBRARY) -o $@ 
		#rm -f *.mod

fftpack.o: %.o: %.f
	${FC} -c ${DEBUG} ${OPTIM} ${WARNING} ${INCLUDE} ${OPTIONS} $< -o $@
%.o: %.f90
	${FC} -c -fcray-pointer ${DEBUG} ${OPTIM} ${WARNING} ${INCLUDE} ${OPTIONS} $< -o $@
	
clean:
	rm -f *.mod *.o
