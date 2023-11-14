# Datas e TimeZone C#

```csharp
/*Console.Clear();
          var data0 = new DateTime(); cria uma nova data, mas ela aparece como 01/01/0001.
          var data1 = DateTime.Now;  pega a hora e data atual da regiao.
          var data2 = new DateTime(2020, 10, 12, 8, 23, 14); cria uma nova data com essses valores 12/10/2020 08:23:14
          var formatada = String.Format("{0:dd/MM/yyyy hh:mm:ss}", data);  aqui ele formata a data de acordo com o que o 
                                                                           desenvolvedor solicitar 

    Console.WriteLine($"{data0}    {data1}    {data2}");
          Console.WriteLine(data0);
          Console.WriteLine(data1);
          Console.WriteLine(data2);
          Console.WriteLine(data1.Year);  obtem somente o ano dessa data
          Console.WriteLine(data1.Month);  obtem somente o mes dessa data
          Console.WriteLine(data1.Day);  obtem somente o dia dessa data
          Console.WriteLine(data1.Hour);  obtem somente as horas dessa data
          Console.WriteLine(data1.Minute);  obtem somente os minutos dessa data
          Console.WriteLine(data1.Second);  obtem somente os segundos dessa data

          Console.WriteLine(data1.DayOfWeek);  obtem o dia da semana dessa data 

          Console.WriteLine(data1.DayOfYear);  obtem o dia do ano

          Console.WriteLine((int)data1.DayOfWeek);  funcao de casting com enumerador, ele pega o numero
                                                     desse dia da semana. ex: 1=domingo, 2=segunda, 3=terça 
    
---------------------------------------------------------------------------------------------------------------------------------    
            Tipos de formatacoes de data
     
            
    var formatada = String.Format("{0:t}", data); = 19:20 . horas compactada (short Time)  
    var formatada = String.Format("{0:T}", data); = 19:23:04 . horas longas 
    var formatada = String.Format("{0:d}", data); = 18/02/2023 . data compactada 
    var formatada = String.Format("{0:D}", data); = sábado, 18 de fevereiro de 2023 . data longa 
    var formatada = String.Format("{0:f}", data); = sábado, 18 de fevereiro de 2023 19:25 . data e hora longa
    var formatada = String.Format("{0:g}", data); = 18/02/2023 19:25 . data e hora curta
    var formatada = String.Format("{0:r}", data); = Sat, 18 Feb 2023 19:28:57 GMT . usado para padroes em sistema
    var formatada = String.Format("{0:s}", data); = 2023-02-18T19:29:53 . usado para o padrao em formato json (usado tbm em no cicle tipo o mongo )
    var formatada = String.Format("{0:u}", data); = 2023-02-18 19:31:53Z . padrao universal, com a zona de area no final
    
---------------------------------------------------------------------------------------------------------------------------------  
            Subtraindo ou adicionando alguma data 

    Console.WriteLine(data);
            Console.WriteLine(data.AddDays(12)); = adiciona a data atual mais 12 dias 
            Console.WriteLine(data.AddDays(-12)); = adiciona a data atual menos 12 dias 
            Console.WriteLine(data.AddMonths(1)); = adiciona a data atual mais 1 mes  
            Console.WriteLine(data.AddYears(1)); = adiciona a data atual mais 1 ano

    podemos subtrair ou adicionar tanto faz (usar sempre esse metodo, pois atualiza automaticamente)

---------------------------------------------------------------------------------------------------------------------------------
            Comparacao de data para entendimento

            
            var data = DateTime.Now;

            if (data == DateTime.Now) {
                Console.WriteLine("e igual");
            }
    nesse exemplo vemos que a infomacao nao e verdadeira, pois o primeiro dateTime e diferente do segundo dateTime, porque apos ele pular para fazer a comparacao ja se passou fracao de segundos e isso faz com que o resultado fique diferente.

    var data = DateTime.Now;

            if (data.Date == DateTime.Now.Date) {
                Console.WriteLine("e igual");
            }
    nesse caso o resultado e igual, pois a data e igual, tbm nao tem a comparacao de tempo, mas somente a de data.
    podemos fazer qualquer tipo de comparacao de data.

---------------------------------------------------------------------------------------------------------------------------------

            Usando o globalization para reconhecer as regioes com data e hora

    var pt = new CultureInfo("pt-PT");
            var br = new CultureInfo("pt-BR");
            var en = new CultureInfo("en-US");
            var de = new CultureInfo("de-DE");
            var atual = CultureInfor.CurrentCulture; = pega a cultura atual da maquina (pode ocorrer de pega a cultura do servidor tbm, se o servidor estiver localizado em outro pais, vai pegar o padrao daquele pais)

            Console.WriteLine(DateTime.Now.ToString("D",pt));
            Console.WriteLine(DateTime.Now.ToString("D", br));
            Console.WriteLine(DateTime.Now.ToString("D", en));
            Console.WriteLine(DateTime.Now.ToString("D", de));

RESULTADO =>     sábado, 18 de fevereiro de 2023
                 sábado, 18 de fevereiro de 2023
                 Saturday, February 18, 2023
                 Samstag, 18.Februar 2023

---------------------------------------------------------------------------------------------------------------------------------
            Fazendo conversao de timeZone, data e hora de acordo com a regiao 

    var utcDate = DateTime.UtcNow;  hora atual em sem timeZone

            Console.WriteLine(DateTime.Now);  data e hora atual da maquina
            Console.WriteLine(utcDate); 
            Console.WriteLine(utcDate.ToLocalTime());  pega o valor da variavel e converte o valor de acordo com timeZone

            var timeZoneAustralia = TimeZoneInfo.FindSystemTimeZoneById("Pacific/Auckland");  aqui ele pega somente o timeZone
            Console.WriteLine(timeZoneAustralia);

            var horaAustralia = TimeZoneInfo.ConvertTimeFromUtc(utcDate, timeZoneAustralia);  ele pega a data e hora, junto com o timeZone que declaramos e junta os dois.
            Console.WriteLine(horaAustralia);

---------------------------------------------------------------------------------------------------------------------------------

    var utcZone = DateTime.UtcNow;
              var timeZones = TimeZoneInfo.GetSystemTimeZones();
            foreach (var timezone in timeZones) {

                Console.WriteLine(timezone.Id);
                Console.WriteLine(timezone);
                Console.WriteLine(TimeZoneInfo.ConvertTimeFromUtc(utcZone,timezone));
                Console.WriteLine("-----------");    

            }

            aqui ele lista todas as regioes e e o timeZone de todos.

---------------------------------------------------------------------------------------------------------------------------------

                Usando o timeSpan (ele serve para tratar horas minutos, segundos, nanoSegundos. para calcular ultilizado normalmente para controle de horas de funcionario de grandes empresas) 

    var timeSpan = new TimeSpan();
             Console.WriteLine(timeSpan);

             var timeSpanNanosegundos = new TimeSpan(1);
             Console.WriteLine(timeSpanNanosegundos);

             var timeSpanHoraMinutoSegundo = new TimeSpan(5, 12, 8);
             Console.WriteLine(timeSpanHoraMinutoSegundo);

             var timeSpanDiaHoraMinutoSegundo = new TimeSpan(3, 5, 50, 10);
             Console.WriteLine(timeSpanDiaHoraMinutoSegundo);

             var timeSpanDiaHoraMinutoSegundoMilissegundo = new TimeSpan(15, 12, 55, 8, 100);
             Console.WriteLine(timeSpanDiaHoraMinutoSegundoMilissegundo);

             Console.WriteLine(timeSpanHoraMinutoSegundo - timeSpanDiaHoraMinutoSegundo);
             Console.WriteLine(timeSpanDiaHoraMinutoSegundo.Days);
             Console.WriteLine(timeSpanDiaHoraMinutoSegundo.Add(new TimeSpan(12, 0, 0)));

            RESULTADO =>    00:00:00
                            00:00:00.0000001
                            05:12:08
                            3.05:50:10
                            15.12:55:08.1000000
                            -3.00:38:02
                            3
                            3.17:50:10

            Console.WriteLine(DateTime.DaysInMonth(2020, 2)); aqui ele quer saber, quantos dias tem o mes de fevereiro do ano de 2020.
            Console.WriteLine(IsWeekend(DateTime.Now.DayOfWeek)); ele mostrar o resultado para saber se hoje e final de semana
            Console.WriteLine(DateTime.Now.IsDaylightSavingTime()); quer saber se estamos no horario de verao
        }

        static bool IsWeekend(DayOfWeek today) { comparando o dia da semana escolhido com o dia de hoje 

            return today == DayOfWeek.Saturday  hoje e igual a sabado || today == DayOfWeek.Sunday;   ou igual a domingo 
    
    tipo booleano vai trazer falso ou verdadeiro caso aquele dia seja fim de semana

    RESULTADO =>    29
                    True
                    False

     */
```
