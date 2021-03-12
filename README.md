# ColegioDanteT
--triggers modo msm "ingreso"
create trigger TRI_estudiante
on estudiante 
for insert
as
print 'se realizo el ingreso de un nuevo estudiante';
go

insert into estudiante values ('1029384912', 'Pepito Mauricio', 'Vera Garcia' ,'M', '2016-10-11', 'Manta','0913456789')

delete from estudiante where nombre='Pepito Mauricio'
select * from estudiante

--triggers modo msm "Eliminacion"
create trigger TRI_estudiante1
on estudiante 
for delete
as
print 'se realizo la eliminacion de un estudiante' 
go
----------------------------------------
declare @nombres varchar(50)
declare @apellidos varchar(50)
declare @fecha varchar(50)

declare cursorest Cursor 
for select estudiante.nombre, estudiante.apellido ,estudiante.fecha_n from estudiante

open cursorest
fetch next from cursorest into @nombres, @apellidos, @fecha

while(@@FETCH_STATUS=0)

		begin
			print 'Nombres completos  ' +@nombres +' '+ @apellidos +' '+ 'fecha de nacimiento '+ @fecha;
			fetch next from cursorest into @nombres, @apellidos, @fecha
	   	end

close cursorest
deallocate cursorest
------------------------------procedimiento almacenado.
if OBJECT_ID('matriculados_total') is not null
begin
	drop procedure matriculados_total
end
go

select * from docente
select * from estudiante
------Procedimiento almacenado 
create procedure SP_edi
@nombreest as varchar (50),
@direccion as varchar (50)
as 
update estudiante set direccion=@direccion
where nombre=@nombreest

select * from estudiante

exec SP_edi 'Karla Manuela','Manta'
