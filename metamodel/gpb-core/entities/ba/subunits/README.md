  # Краткое описание
  
  На момент формирования модели предполагается, что есть несколько связанных организационных типов (type):
  1. *su* - Подразделение
  2. *vs* - Value Stream
  3. *block* - Блок
  4. *cluster* - Кластер
  
  Последний элемент в иерархии является группировкой для систем и если требуется сгруппировать системы в разрезе этого элемента, то необходимо указать его идентификатор в значение реквизита системы *subunit:*.

  Также этот элемент можно использовать для оптимизации процесса ввода следующих реквизитов системы:
    * business_owners
    * application_owner
    * architect
    * budget_holder
    * business_areas (на момент написания инструкции используется system_category, но он будет заменен на business_areas)