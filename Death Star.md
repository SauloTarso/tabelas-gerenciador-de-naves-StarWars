```
use EstrelaDaMorte

create table Planetas
(
	IdPlaneta int not null,
	Nome varchar(50) not null,
	Rotacao float not null,
	Diametro float not null,
	Clima varchar(50) not null,
	Populacao int not null,
)
go

alter table Planetas add constraint PK_Planetas primary key (IdPlaneta);


create table Nave
(
	IdNave int not null,
	Nome varchar(50) not null,
	Modelo varchar(50) not null,
	Passageiros int not null,
	Carga float not null,
	Classe varchar(50)
)
go

alter table Nave add constraint PK_Nave primary key (IdNave);


create table Pilotos
(
	IdPiloto int not null,
	Nome varchar(100) not null,
	AnoNascimento varchar(10) not null,
	IdPlaneta int not null,
)
go

alter table Pilotos add constraint PK_Pilotos primary key (IdPiloto);`
go

alter table Pilotos add constraint FK_Pilotos_Planetas foreign key (IdPlaneta)
references Planetas (IdPlaneta)


create table PilotosNaves
(
	IdPiloto int not null,
	IdNave int not null,
	FlagAutorizado bit not null,
)
go
	
alter table PilotosNaves add constraint PK_PilotosNaves primary key (IdPiloto, IdNave);
	go
	
alter table PilotosNaves add constraint FK_PilotosNaves_Pilotos foreign key (IdPiloto) references Pilotos (IdPiloto)
go

alter table PilotosNaves add constraint FK_PilotosNaves_Naves foreign key (IdNave) references Nave (IdNave)
go

alter table PilotosNaves add constraint DF_PilotosNaves_FlagAutorizado default (1) for FlagAutorizado

create table HistoricoViagens
(
	IdNave int not null,
	IdPiloto int not null,
	DtSaida datetime not null,
	DtChegada datetime null,
)
go

alter table HistoricoViagens add constraint FK_HistoricoViagens_PilotosNaves foreign key (IdPiloto, IdNave)
references PilotosNaves (IdPiloto, IdNave)
go

alter table HistoricoViagens check constraint FK_HistoricoViagens_PilotosNaves

select * from Pilotos
select * from Planetas
select * from Nave
select * from PilotosNaves
select * from HistoricoViagens
```

