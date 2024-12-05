# <p align="center">Banco de dados em java (Execução dos códigos)
### <p align="center">Trabalho de integração de dados PostgreSQL usando Java</p>

#### Conectando driver do PostgreSQL:
```
  public class ConectandoDriverSQL {
      static String driverJDBC = "org.postgresql.Driver";
      public static void main(String[] args){
          try{
              
              System.out.println("Carregando driver JDBC...");
              Class.forName(driverJDBC);
              System.out.println("Driver Carregado!");
              
          }catch(Exception error){
              System.out.printf("Falha no carregamento! %c",error);
          }
      }   
  }
```
[![Conectando-Drive.png](https://i.postimg.cc/Gmn7V7x6/Conectando-Drive.png)](https://postimg.cc/2VT7BxJx)
***

#### Conectado ao Banco de Dados SQL:
```
import java.sql.Connection;
import java.sql.DriverManager;
import java.sql.SQLException;

public class ConectandoBDSQL{
    
  public static void main(String[] args) {
    String driver = "jdbc:postgresql://127.0.0.1:5432/DadosGerais";
    try (Connection conn = DriverManager.getConnection(driver, "postgres", "75716123")) {
      if (conn != null) {
        System.out.println("Conectado ao banco de dados!");
      } else {
        System.out.println("Falhou em fazer a conexão");
      }
    }catch (SQLException e){
      System.err.format("SQL State: %s\n%s",e.getSQLState(), e.getMessage());
    }
  }
}

```
[![Conectando-BD.png](https://i.postimg.cc/SNsn5xYH/Conectando-BD.png)](https://postimg.cc/G9W3TrQj)
***

####  Criando tabela do Banco de Dados:
```
import java.sql.Connection;
import java.sql.DriverManager;
import java.sql.SQLException;
import java.sql.Statement;

public class CriandoTabelaSQL {
    public static void main(String[] args) {
        String SQLcriarTabela = "CREATE TABLE pessoa (cpf int, nome VARCHAR(60))";
        String driver = "jdbc:postgresql://127.0.0.1:5432/DadosGerais";
        Statement st = null;
        
        try(Connection conn = DriverManager.getConnection(driver,"postgres","75716123")){
            if(conn != null){
                System.out.println("Connected to the database!");
            }else{
                System.out.println("Failed to make connection!");
            }
            
            System.out.println("Criando tabela, aguarde...");
            st = conn.createStatement();
            st.executeUpdate(SQLcriarTabela);
            
            System.out.println("Tabela criada c/ sucesso!");
            st.close();
            conn.close();
            
        }catch (SQLException error){
            System.err.format("SQL State: %s\n%s", error.getSQLState(), error.getMessage());
        }
    }
}
    

```
[![Criando-Tabela-BD.png](https://i.postimg.cc/SNvf15R7/Criando-Tabela-BD.png)](https://postimg.cc/sv5WvTpv)
***

####  Inserindo os dados na tabela:
```
import java.sql.Connection;
import java.sql.DriverManager;
import java.sql.SQLException;
import java.sql.Statement;

public class InserindoDadosSQL {
    public static void main(String[] args) {
        String SQLinserirDados = "INSERT INTO pessoa (cpf, nome) VALUES (23145712 , 'maria maria')";
        String driver = "jdbc:postgresql://127.0.0.1:5432/DadosGerais";
        Statement st = null;
    
        try(Connection conn = DriverManager.getConnection(driver, "postgres","75716123")) {
            if(conn != null){
                System.out.println("Connected to the database!");
            }else{
                System.out.println("Failed to make connection!");
            }
            
            System.out.println("Inserindo Dados na Tabela...");
            st = conn.createStatement();
            st.executeUpdate(SQLinserirDados);
            
            System.out.println("Dados inseridos!");
            st.close();
            conn.close();
            
        }catch(SQLException error){
            System.err.format("SQL State: %s\n%s", error.getSQLState(), error.getMessage());
        }
    }
}

```
[![Inserindo-Dados-BD.png](https://i.postimg.cc/525jQYhY/Inserindo-Dados-BD.png)](https://postimg.cc/RWFvjFV4)
***

####  Consultado os dados após a inserção de dados na tabela: 
```
import java.sql.Connection;
import java.sql.DriverManager;
import java.sql.SQLException;
import java.sql.Statement;
import java.sql.ResultSet;

public class ConsultandoDadosSQL {
    public static void main(String[] args) {
        String SQLconsultarDados = "Select * from pessoa";
        String driver = "jdbc:postgresql://127.0.0.1:5432/DadosGerais";
        Statement st;
        ResultSet result;
        
        try(Connection conn = DriverManager.getConnection(driver, "postgres","75716123")) {
            if(conn != null){
                System.out.println("Connected to the database!");
            }else{
                System.out.println("Failed to make connection!");
            }
            
            System.out.println("Consultando dados na Tabela...");
            st = conn.createStatement();
            result = st.executeQuery(SQLconsultarDados);
            
            while (result.next()){
            System.out.println("--------------------------");
            System.out.println("CPF: " + result.getString(1));
            System.out.println("Nome: " + result.getString(2));
        }
            
        result.close();
        st.close();
        conn.close();
        
        }catch(SQLException error){
            System.err.format("SQL State: %s\n%s", error.getSQLState(), error.getMessage());       
        }  
    }
}
```
[![Consultando-Dados1-BD.png](https://i.postimg.cc/wMK7sXjN/Consultando-Dados1-BD.png)](https://postimg.cc/WFn2BJrp)
***

####  Atualizando os dados da tabela:
```
import java.sql.Connection;
import java.sql.DriverManager;
import java.sql.SQLException;
import java.sql.Statement;

public class AtualizandoDadosSQL {
        public static void main(String[] args) {
            String SQLatualizarDados = "update pessoa set nome = 'Carlos'";
            String driver = "jdbc:postgresql://127.0.0.1:5432/DadosGerais";
            Statement st = null;
            
            try(Connection conn = DriverManager.getConnection(driver, "postgres","75716123")) {
            if(conn != null){
                System.out.println("Connected to the database!");
            }else{
                System.out.println("Failed to make connection!");
            }
            
            System.out.println("Atualizando dados na Tabela...");
            st = conn.createStatement();
            st.executeUpdate(SQLatualizarDados);
            
            System.out.println("Dados atualizados!");
            st.close();
            conn.close();
            
        }catch(SQLException error){
            System.err.format("SQL State: %s\n%s", error.getSQLState(), error.getMessage());
        }
    }
}
```
[![Atualizando-Dados-BD.png](https://i.postimg.cc/1zk9W91h/Atualizando-Dados-BD.png)](https://postimg.cc/hJ0WvRGp)
***

####  Excluindo os dados das tabela:
```
import java.sql.Connection;
import java.sql.DriverManager;
import java.sql.SQLException;
import java.sql.Statement;

public class ExcluindoDadosSQL {
        public static void main(String[] args) {
            String SQLexcluirDados = "DELETE from pessoa";
            String driver = "jdbc:postgresql://127.0.0.1:5432/DadosGerais";
            Statement st = null;
            
            try(Connection conn = DriverManager.getConnection(driver, "postgres","75716123")) {
            if(conn != null){
                System.out.println("Connected to the database!");
            }else{
                System.out.println("Failed to make connection!");
            }
            
            System.out.println("Excluindo dados da Tabela...");
            st = conn.createStatement();
            st.executeUpdate(SQLexcluirDados);
            
            System.out.println("Dados Excluídos!");
            st.close();
            conn.close();
            
        }catch(SQLException error){
            System.err.format("SQL State: %s\n%s", error.getSQLState(), error.getMessage());
        }        
    }   
}
```
[![Excluindo-Dados-BD.png](https://i.postimg.cc/JnXjg4yb/Excluindo-Dados-BD.png)](https://postimg.cc/Fd9fkvVR)
***
