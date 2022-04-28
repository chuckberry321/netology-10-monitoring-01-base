# 10.01. Зачем и что нужно мониторить

### 1. Вас пригласили настроить мониторинг на проект. На онбординге вам рассказали, что проект представляет из себя платформу для вычислений с выдачей текстовых отчетов, которые сохраняются на диск. Взаимодействие с платформой осуществляется по протоколу http. Также вам отметили, что вычисления загружают ЦПУ. Какой минимальный набор метрик вы выведите в мониторинг и почему?

  **Ответ:**   
+  скорость записи/чтения на диск - чтобы вовремя исключить деградацию дисков   
+  свободное место на диске - чтобы не потерять данные при переполнении хранилища и обсепечить долговечность и быстродействие
+  количество http запросов - определение нагрузки на систему
+  время ответа http (http response time) - определение времени обработки запросов сервером
+  коды ответа HTTP (http responce code) - определение правильности работы кода, запросов и количества не успещно выполненных запросов
+  средние значения нагрузки (Load averages) - чтобы оценить динамику нагрузки и вовремя масштабировать систему
+  показатель iowait - для контроля времени ответа системы    
   Таким образом мы будем использовать и "четыре золотых сигнала"

### 2. Менеджер продукта посмотрев на ваши метрики сказал, что ему непонятно что такое RAM/inodes/CPUla. Также он сказал, что хочет понимать, насколько мы выполняем свои обязанности перед клиентами и какое качество обслуживания. Что вы можете ему предложить?

  **Ответ:**   
  Объяснить, что : RAM  - это объем оперативной памяти хоста, indoes - кол-во файловых дескрипторов, которые хранят информацию о файлах системыи, CPUla - загрузка процессора   
  Предлложить  SLO - 99%, дополнительные метрики - если речь об отчетах в первом вопросе, то метрики по времени на формирование отчетов в среднем и в пиковых значениях, чтобы определить наибольшую нагрузку,
статиктику по неудачно сформированным отчетам, доступность сервиса.

### 3. Вашей DevOps команде в этом году не выделили финансирование на построение системы сбора логов. Разработчики в свою очередь хотят видеть все ошибки, которые выдают их приложения. Какое решение вы можете предпринять в этой ситуации, чтобы разработчики получали ошибки приложения?

  **Ответ:**   
  Я бы, скорее всего, использовал бесплатный ELK с дашбордами Kibana.

### 3. Вы, как опытный SRE, сделали мониторинг, куда вывели отображения выполнения SLA=99% по http кодам ответов. Вычисляете этот параметр по следующей формуле: summ_2xx_requests/summ_all_requests. Данный параметр не поднимается выше 70%, но при этом в вашей системе нет кодов ответа 5xx и 4xx. Где у вас ошибка?

  **Ответ:**   
  В расчете SLA, кроме кодов 2xx должны учитываться коды  3xx (коды перенаправления) и 1xx (информационные коды)   
  Формула должна вглыдяеть так - (summ_1xx_requests + summ_2xx_requests + summ_3xx_requests)/(summ_all_requests)
