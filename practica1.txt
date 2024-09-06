@echo off
:menu
cls
echo =======================
echo  Gestor de Horarios
echo =======================
echo 1. Agregar Materia y Horario
echo 2. Eliminar Materia
echo 3. Mostrar Horario
echo 4. Eliminar Todo el Horario
echo 5. Guardar Horario en PDF
echo 6. Salir
echo =======================
set /p choice="Elija una opción: "

if "%choice%"=="1" goto agregar
if "%choice%"=="2" goto eliminar
if "%choice%"=="3" goto mostrar
if "%choice%"=="4" goto eliminar_todo
if "%choice%"=="5" goto guardar_pdf
if "%choice%"=="6" exit

goto menu

:agregar
cls
set /p materia="Ingrese el nombre de la materia: "
set /p hora="Ingrese el horario (Ej: 3:00-4:00): "
rem Formatear la salida con la materia y hora con alineación
echo %materia%             %hora% >> horario.txt
echo Materia y horario agregados!
pause
goto menu

:eliminar
cls
type horario.txt
set /p delete="Ingrese el nombre de la materia que desea eliminar: "
findstr /v /c:"%delete%" horario.txt > temp.txt
move temp.txt horario.txt
echo Materia eliminada!
pause
goto menu

:mostrar
cls
echo ======= Horario =======
type horario.txt
echo =======================
pause
goto menu

:eliminar_todo
cls
echo Está seguro de que desea eliminar todo el horario? (S/N)
set /p confirm="Ingrese su elección: "
if /i "%confirm%"=="S" (
    echo. > horario.txt
    echo Todo el horario ha sido eliminado!
) else (
    echo Operación cancelada.
)
pause
goto menu

:guardar_pdf
cls
echo Guardando en PDF...
rem Este paso depende de tener una herramienta de conversión o la impresora "Microsoft Print to PDF"
notepad.exe /p horario.txt
pause
goto menu