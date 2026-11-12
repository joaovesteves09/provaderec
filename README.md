--  create table investidores (
-- id serial primary key,
-- nome varchar (100) not null,
		-- cpf char (11) unique not null,
		-- nivel_experiencia integer default 0 check (nivel_experiencia >= 0)
-- );

-- create table carteira (
-- id serial primary key,
-- investidor_id integer references investidores(id),
-- endereço_wallet varchar (100) unique not null,
-- rede_blockhain varchar (50) not null,
-- saldo_usd decimal (15,2)not null check (saldo_usd >=0),
-- status varchar (20) default 'ativa'
-- check (status in('ativa','em analise','bloqueada','pausada'))
-- );

-- create table corretoras (
-- id serial primary key, 
-- nome_exchange varchar(100) not null,
-- cpnj char (14) unique not null,
-- email_suporte varchar (100) unique not null
-- );

-- create table criptomoedas (
-- id serial primary key,
-- corretora_id integer references corretoras(id),
-- nome_moeda varchar (50) not null,
-- preco_unitario_usd decimal (15,2) not null check (preco_unitario_usd > 0),
-- categoria varchar (20) default 'layer1'
-- check (categoria in('layer1','defi','memecoin','stablecoin'))
-- );

-- create table transacoes_criptomoedas (
--     id serial primary key,
--     carteira_ID integer references criptomoedas(id),
--     criptomoedas_id integer references criptomoedas(ID),
--     quantidade decimal (15,8) not null check (quantidade > 0),
--     valor_pago decimal (15,2) not null check (valor_pago > 0),
--     data_transacao timestamp default current_timestamp not null
-- );
-- INSERT INTO investidores (nome, cpf, nivel_experiencia) VALUES
-- ('Joao Silva', '12345678911', 2),
-- ('Maria Santos', '23456789112', 5),
-- ('Pedro Costa', '34567890121', 1),
-- ('Ana Oliveira', '45678901214', 3),
-- ('Lucas Souza', '56789012145', 4);
--
--(1, '0x71C7656EC7ab88b098defB751B7401B5f6d8976F', 'Ethereum', 1500.50, 'ativa'),
--(2, '1A1zP1eP5QGefi2DMPTfTL5SLmv7DivfNa', 'Bitcoin', 8200.00, 'ativa'),
--(3, '0x3fC91A3afd70395Cd496C647d5a6CC9D4B2b7FAD', 'Solana', 450.00, 'em analise'),
--(4, '0x89205A3A3b2A69De6Dbf7f01ED13B2108B2c43e7', 'Ethereum', 12500.75, 'bloqueada'),
--(5, '0xd8dA6BF26964aF9D7eEd9e03E53415D37aA96045', 'Polygon', 90.00, 'pausada');


-- INSERT INTO corretoras (nome_exchange, cnpj, email_suporte) VALUES
-- ('Binance Brasil', '12345678000195', 'suporte@binance.com.br'),
-- ('Mercado Bitcoin', '98765432000188', 'ajuda@mercadobitcoin.com.br'),
-- ('Coinbase', '45678912000177', 'support@coinbase.com'),
-- ('Foxbit', '78912345000166', 'contato@foxbit.com.br'),
-- ('Kraken', '32165498000155', 'support@kraken.com');


--INSERT INTO criptomoeda (corretora_id, nome_moeda, preco_unitario_usd, categoria) VALUES
--(1, 'Bitcoin', 65000.00, 'Layer1'),
--(1, 'Ethereum', 3500.00, 'Layer1'),
--(2, 'Uniswap', 8.50, 'DeFi'),
--(3, 'USD Coin', 1.00, 'Stablecoin'),
--(4, 'Dogecoin', 0.12, 'Memecoin');


--INSERT INTO transacoes_criptomoedas (carteira_id, criptomoedas_id, quantidade, valor_pago) VALUES
--(1, 1, 0.05000000, 3250.00),
--(2, 2, 2.00000000, 7000.00),
--(3, 3, 50.00000000, 425.00),
--(4, 1, 0.01000000, 650);

-- create view vw_painel_carteiras as
-- select
--     c.endereco_wallet,
--     c.rede_blockchain,
--     c.status,
--     c.saldo_usd,
--     i.nome as nome_investidor,
--     i.cpf
-- from carteiras c
-- inner join investidores i on c.investidor_id = i.id; 


-- create view vw_investimento_total_carteiras as
-- select
--     c.id as id_carteira,
--     c.endereco_wallet,
--     c.saldo_usd,
--     count(t.id) as quantidade_transacoes,
--     coalesce(sum(t.valor_pago), 0) as custo_total
-- from carteiras c
-- left join transacoes_cripto t on c.id = t.carteira_id
-- group by c.id, c.endereco_wallet, c.saldo_usd;
