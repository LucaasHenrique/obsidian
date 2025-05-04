Stored procedures são rotinas definidas no banco de dados, identificadas por um nome pelo qual podem ser invocadas. Este procedimento pode receber parâmetros, retornar valores e executar uma sequência de instruções, por exemplo: fazer update em uma tabela e, em sequência, inserir em outra e retornar um resultado de uma conta para sua aplicação.

procedure$$
create procedure atualizar_salario(
	in id_cliente int
)
begin
	declare salario float;
    declare newSalario float;
	
    select salario into salario from clientes where id_cliente = id_cliente limit 1;
    
    select concat('Salário atual: ', salario) as debug;
	
    if salario is not null then
		if (salario < 3000) then
			set newSalario = salario * 1.1;
		else
			set newSalario = salario * 1.05;
		end if;
		select concat('Novo salário: ', newSalario) as debug;
        update clientes set salario = newSalario where id_cliente = id_cliente;
        commit;
        
		select 'Salário atualizado com sucesso!' as debug;
    else
        -- Log: Se o salário for nulo ou o ID não existir
        select 'Erro: Salário não encontrado ou ID inválido.' as debug;
        
	end if;
end$$
call atualizar_salario(4);
