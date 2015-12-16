# FAST 6.01 MEX,EXE Manual makefile
# Author: 	Stefano Cottafavi 
# Date: 	07/2008
# Last mod: 03/2010 
# Notes:  	Eclipse + Photran + G95 FORTRAN compiler

# Folders
ROOT 	= ..
SRCF	= ${ROOT}/Source
SRCA	= ${SRCF}/aerodyn
SRCS	= ${SRCF}/simulink
SRCH	= ${SRCF}/helpers

# Configuration options
NAME  = FAST601.exe
NAMEs = FAST601_SFunc.mexw32
OUT  = objects

# Commands
FC 		= g95
DEBUG	= 
OPTIM	= -O0 
WARNING	= -Wno-line-truncation
INCLUDE = #-I"C:\Programmi\MATLAB\R2007b\extern\include" 			#"C:\Programmi\MATLAB\R2008b\extern\include"
LIBRARY	= #-L"C:\Programmi\MATLAB\R2007b\bin\win32" -lmex -lmat -lmx #"C:\Programmi\MATLAB\R2008b\bin\win32" -lmex -lmat -lmx
MACRO 	= #-DMATLAB_MEX_FILE
OPTIONS	= -fmod=modules -ffree-line-length-huge -fno-underscoring #-fcase-upper #-r8 
MACHINE	= 
OUTPUT 	= 

# Compiler flags (CFLAGS), Linker flags (LFLAGS)
CFLAGS	= -c ${DEBUG} ${OPTIM} ${WARNING} ${INCLUDE} ${OPTIONS}


# Targets: Executable, S-Function
FAST:	ModG95.o SysG95.o \
		fftpack.o FFTMod.o \
		AeroMods.o NoiseMods.o FastMods.o \
		AeroSubs.o GenSubs.o NoiseSubs.o UserSubs.o \
		GenUse.o SetVersion.o \
		AeroCalc.o HydroCalc.o FastIO.o FAST2ADAMS.o FAST_Lin.o \
		PitchControl.o SpeedControl.o UserWind.o \
		Fast.o FastProg.o
		
		${FC} \
		-o $(NAME) \
		$(OUT)/ModG95.o $(OUT)/SysG95.o \
		$(OUT)/fftpack.o $(OUT)/FFTMod.o \
		$(OUT)/AeroMods.o $(OUT)/NoiseMods.o $(OUT)/FastMods.o \
		$(OUT)/GenSubs.o $(OUT)/AeroSubs.o $(OUT)/NoiseSubs.o $(OUT)/UserSubs.o \
		$(OUT)/GenUse.o $(OUT)/SetVersion.o \
		$(OUT)/HydroCalc.o $(OUT)/AeroCalc.o $(OUT)/FastIO.o $(OUT)/FAST2ADAMS.o $(OUT)/FAST_Lin.o \
		$(OUT)/PitchControl.o $(OUT)/SpeedControl.o $(OUT)/UserWind.o \
		$(OUT)/Fast.o $(OUT)/FastProg.o
		
FASTs:	ModG95.o SysG95.o \
		fftpack.o \
		AeroModsS.o FFTMod.o NoiseMods.o FastMods.o \
		AeroSubs.o GenSubsS.o NoiseSubs.o UserSubs.o \
		GenUse.o SetVersion.o \
		AeroCalc.o HydroCalc.o FastIO.o FAST2ADAMS.o FAST_Lin.o \
		PitchControl.o SpeedControl.o UserWind.o \
		Fast.o FastDynamics.o FastGateway.o makefile
		
		${FC} -shared ${MACRO} ${LIBRARY} ${MACHINE} ${OUTPUT} \
		-o $(NAMEs) \
		$(OUT)/ModG95.o $(OUT)/SysG95.o \
		$(OUT)/fftpack.o \
		$(OUT)/AeroModsS.o $(OUT)/FFTMod.o $(OUT)/NoiseMods.o $(OUT)/FastMods.o \
		$(OUT)/GenSubsS.o $(OUT)/AeroSubs.o $(OUT)/NoiseSubs.o $(OUT)/UserSubs.o \
		$(OUT)/GenUse.o $(OUT)/SetVersion.o \
		$(OUT)/HydroCalc.o $(OUT)/AeroCalc.o $(OUT)/FastIO.o $(OUT)/FAST2ADAMS.o $(OUT)/FAST_Lin.o \
		$(OUT)/PitchControl.o $(OUT)/SpeedControl.o $(OUT)/UserWind.o \
		$(OUT)/Fast.o $(OUT)/FastDynamics.o $(OUT)/FastGateway.o

#clean:
#		rm -f *.mod *.o

# -- COMPILE	
ModG95.o: $(SRCH)/ModG95.f90 makefile
	${FC} ${CFLAGS} $(SRCH)/ModG95.f90 -o $(OUT)/$@	
SysG95.o: $(SRCH)/SysG95.f90 makefile
	${FC} ${CFLAGS} $(SRCH)/SysG95.f90 -o $(OUT)/$@
	
FastDynamics.o:	${SRCS}/FASTDynamics.f90 makefile
	${FC} ${CFLAGS} ${SRCS}/FASTDynamics.f90 -o ${OUT}/$@
FastGateway.o:	${SRCS}/FastGateway.f90 makefile
	${FC} ${CFLAGS} ${SRCS}/FastGateway.f90 -o ${OUT}/$@

fftpack.o: $(SRCF)/fftpack.f makefile
	${FC} ${CFLAGS} $(OPT) $(SRCF)/fftpack.f -o $(OUT)/$@
FFTMod.o: $(SRCF)/FFTMod.f90 makefile
	${FC} ${CFLAGS} $(OPT) $(SRCF)/FFTMod.f90 -o $(OUT)/$@

AeroMods.o:	$(SRCA)/AeroMods.f90 makefile
	${FC} ${CFLAGS} $(SRCA)/AeroMods.f90 -o $(OUT)/$@
AeroModsS.o:	$(SRCS)/AeroMods_SFunc.f90 makefile
	${FC} ${CFLAGS} $(SRCS)/AeroMods_SFunc.f90 -o $(OUT)/$@
NoiseMods.o: $(SRCF)/NoiseMods.f90 makefile
	${FC} ${CFLAGS} $(SRCF)/NoiseMods.f90 -o $(OUT)/$@
FastMods.o:	$(SRCF)/FAST_Mods.f90 makefile
	${FC} ${CFLAGS} $(SRCF)/FAST_Mods.f90 -o $(OUT)/$@
GenSubs.o: $(SRCA)/GenSubs.f90 makefile
	${FC} ${CFLAGS} $(SRCA)/GenSubs.f90 -o $(OUT)/$@
GenSubsS.o: $(SRCS)/GenSubs_SFunc.f90 makefile
	${FC} ${CFLAGS} $(SRCS)/GenSubs_SFunc.f90 -o $(OUT)/$@
AeroSubs.o:	$(SRCA)/AeroSubs.f90 makefile
	${FC} ${CFLAGS} $(SRCA)/AeroSubs.f90 -o $(OUT)/$@
NoiseSubs.o: $(SRCF)/NoiseSubs.f90 makefile
	${FC} ${CFLAGS} $(SRCF)/NoiseSubs.f90 -o $(OUT)/$@
UserSubs.o: $(SRCF)/UserSubs.f90 makefile
	${FC} ${CFLAGS} $(SRCF)/UserSubs.f90 -o $(OUT)/$@	

SetVersion.o: $(SRCF)/SetVersion.f90 makefile
	${FC} ${CFLAGS} $(SRCF)/SetVersion.f90 -o $(OUT)/$@
GenUse.o: $(SRCF)/GenUse.f90 makefile
	${FC} ${CFLAGS} $(SRCF)/GenUse.f90 -o $(OUT)/$@
		
FastIO.o: $(SRCF)/Fast_IO.f90 makefile
	${FC} ${CFLAGS} $(SRCF)/Fast_IO.f90 -o $(OUT)/$@
AeroCalc.o:	$(SRCF)/AeroCalc.f90 makefile
	${FC} ${CFLAGS} $(SRCF)/AeroCalc.f90 -o $(OUT)/$@
HydroCalc.o: $(SRCF)/HydroCalc.f90 makefile
	${FC} ${CFLAGS} $(SRCF)/HydroCalc.f90 -o $(OUT)/$@
FAST2ADAMS.o: $(SRCF)/FAST2ADAMS.f90 makefile
	${FC} ${CFLAGS} $(SRCF)/FAST2ADAMS.f90 -o $(OUT)/$@
FAST_Lin.o:	$(SRCF)/FAST_Lin.f90 makefile
	${FC} ${CFLAGS} $(SRCF)/FAST_Lin.f90 -o $(OUT)/$@

UserWind.o: $(SRCA)/UserWind.f90 makefile
	${FC} ${CFLAGS} $(SRCA)/UserWind.f90 -o $(OUT)/$@	
PitchControl.o:	$(SRCF)/PitchCntrl_ACH.f90 makefile
	${FC} ${CFLAGS} $(SRCF)/PitchCntrl_ACH.f90 -o $(OUT)/$@
SpeedControl.o:	$(SRCF)/UserVSCont_KP.f90 makefile
	${FC} ${CFLAGS} $(SRCF)/UserVSCont_KP.f90 -o $(OUT)/$@

Fast.o:	$(SRCF)/FAST.f90 makefile
	${FC} ${CFLAGS} $(SRCF)/FAST.f90 -o $(OUT)/$@
FastProg.o:	$(SRCF)/FAST_Prog.f90 makefile
	${FC} ${CFLAGS} $(SRCF)/FAST_Prog.f90 -o $(OUT)/$@


