# Выполнено ДЗ №

 - [x] Основное ДЗ
 - [x] Задание со *

## В процессе сделано:
 - Ответ на вопрос: Почему обновление ReplicaSet не повлекло обновление запущенных pod?
В ReplicaSet не предусмотрено использование rolling update, поэтому обновления подов не произошло.
 - Создан ReplicaSet сервиса frontend. Изменено количество реплик до 3 двумя способами: командой kubectl scale replicaset, а затем редактированием манифеста. 
 - Собрана новая версия микросервиса frontend, после чего эта версия была применена в манифесте ReplicaSet. После применения обновленного манифеста выяснила, что ReplicaSet не производит обновления текущих работающих подов. 
 - Собрано два image микросервиса paymentservice. Созданы манифесты ReplicaSet и Deployment для paymentservice. 
 - Выяснила, что при применении обновленного Deployment применяется стратегия обновления Rolling Update, которая заменяет поды со старой версией на поды с новой версией. 
 - Написано два манифеста Deployment с реализацией сценариев развертывания blue-green и Rolling Update
 - Для микросервиса frontend создан Deployment с readinessProbe. Узнала, что после применения обновленного манифеста Deployment не будет пытаться продолжить обновление, пока readinessProbe для нового пода не станет успешной.
 - Создан и применен манифест node-exporter-daemonset.yaml для развертывания DaemonSet с Node Exporter. На локалхост проброшен порт 9100 из пода node-exporter, после чего по url localhost:9100/metrics стали доступны метрики. 
 - DaemonSet node-exporter-daemonset.yaml модернизирован таким образом, чтобы Node Exporter был развернут не только на worker, так и на master (control-plane) ноде.

## Как запустить проект:
```
 - kubectl apply -f node-exporter-daemonset.yaml 
 - kubectl port-forward node-exporter-*** 9100:9100
```

## Как проверить работоспособность:
 - Перейти по ссылке localhost:9100/metrics 

## PR checklist:
 - [x] Выставлен label с темой домашнего задания
