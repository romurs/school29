<script setup lang="ts">
import { ref } from "vue";

useHead({
  title: "Заказать справку | 29",
  meta: [{ name: "order a certificate", content: "Заказ справок школы номер 29" }],
});

const fio = ref("");
const classNumber = ref("");
const classLetter = ref("");

const fioError = ref(false);
const classError = ref(false);

const validateRussianText = (value: string): boolean => {
  // eslint-disable-next-line no-useless-escape
  const russianRegex = /^[А-Яа-яЁё\s\-]+$/;
  return russianRegex.test(value);
};

const validateFIO = (value: string): boolean => {
  const words = value
    .trim()
    .split(/\s+/)
    .filter((word) => word.length > 0);

  return words.length === 3 && validateRussianText(value);
};

const handleFIOChange = (event: Event) => {
  const target = event.target as HTMLInputElement;
  const value = target.value;

  if (/[0-9A-Za-z]/.test(value)) {
    fioError.value = true;
    return;
  }

  fio.value = value;
  fioError.value = false;
};

const validateForm = (): boolean => {
  let isValid = true;

  if (!validateFIO(fio.value)) {
    fioError.value = true;
    isValid = false;
  }

  if (!classNumber.value || !classLetter.value) {
    classError.value = true;
    isValid = false;
  } else {
    classError.value = false;
  }

  return isValid;
};

const submitForm = async (event: Event) => {
  event.preventDefault();

  if (!validateForm()) {
    return;
  }

  const formData = {
    fio: fio.value.trim(),
    student_class: `${classNumber.value}${classLetter.value}`,  // обратите внимание на class_name вместо class
  };

  try {
    const response = await fetch("http://localhost:8000/api/references/order/", {
      method: "POST",
      headers: {
        "Content-Type": "application/json",
      },
      body: JSON.stringify(formData),
    });

    if (!response.ok) {
      throw new Error(`Ошибка ${response.status}`);
    }

    const data = await response.json();
    console.log("Ответ от сервера:", data);

    // очистка формы
    fio.value = "";
    classNumber.value = "";
    classLetter.value = "";
    fioError.value = false;
    classError.value = false;

    alert("Форма успешно отправлена!");
  } catch (error) {
    console.error("Ошибка при отправке формы:", error);
    alert("Ошибка при отправке. Попробуйте снова.");
  }
};

const classNumbers = Array.from({ length: 11 }, (_, i) => i + 1);
const classLetters = [
  "а", "б", "в", "г", "д", "е", "ж", "з", "и", "к",
  "л", "м", "н", "о", "п", "р", "с", "т", "у", "ф",
  "х", "ц", "ч", "ш", "щ", "э", "ю", "я"
];
</script>


<template>
  <div class="form-container">
    <h1>Заказ справки об обучении ребенка</h1>
    <form @submit="submitForm">
      <div class="form-group">
        <h3>ФИО</h3>
        <input
          type="text"
          v-model="fio"
          @input="handleFIOChange"
          placeholder="Введите ФИО"
          title="Только русские буквы, пробелы и дефисы"
          required
          :class="{ 'error-border': fioError }"
        />
        <div v-if="fioError" class="error">
          Введите Фамилию, Имя и Отчество на русском языке (Пример: Иванов Иван Иванович)
        </div>
      </div>

      <div class="form-group class-selectors">
        <h3>Класс</h3>
        <div class="select-row">
          <select v-model="classNumber" class="class-select" required :class="{ 'error-border': classError && !classNumber }">
            <option value="" disabled selected>Выберите цифру</option>
            <option v-for="num in classNumbers" :key="num" :value="num">
              {{ num }}
            </option>
          </select>
          <select v-model="classLetter" class="class-select" required :class="{ 'error-border': classError && !classLetter }">
            <option value="" disabled selected>Выберите букву</option>
            <option v-for="letter in classLetters" :key="letter" :value="letter">
              {{ letter.toUpperCase() }}
            </option>
          </select>
        </div>
        <div v-if="classError" class="error">
          Пожалуйста, выберите и цифру, и букву класса
        </div>
      </div>

      <button type="submit">Заказать</button>
    </form>
  </div>
</template>

<style scoped lang="scss">
h1 {
  color: black;
  text-align: center;
  margin-bottom: 20px;
  font-size: 24px;
}

.form-container {
  max-width: 400px;
  margin: auto;
  padding: 30px;
  padding-top: 20px;
  border-radius: 12px;
  background: #f9f9f9;
  box-shadow: 0 4px 12px rgba(0, 0, 0, 0.1);
  font-weight: 700;
}

.form-container h3 {
  margin-bottom: 8px;
  font-size: 16px;
  color: #333;
}

.form-group {
  margin-bottom: 20px;
  width: 100%;
}

.class-selectors {
  .select-row {
    display: flex;
    gap: 10px;
    align-items: center;
  }
  
  .class-select {
    flex: 1;
    padding: 10px;
    border: 1px solid #ccc;
    border-radius: 8px;
    font-size: 14px;
    background: white;
    cursor: pointer;
    transition: border 0.3s, box-shadow 0.3s;
    font-weight: 400;
    
    &:focus {
      outline: none;
      border-color: #5ab900;
      box-shadow: 0 0 5px rgba(90, 185, 0, 0.5);
    }
    
    &:invalid {
      color: #999;
    }
    
    option {
      color: #333;
    }
  }
}

.error {
  color: #d32f2f;
  font-size: 13px;
  margin-top: 4px;
  font-weight: 400;
}

.error-border {
  border-color: #d32f2f !important;
  box-shadow: 0 0 5px rgba(211, 47, 47, 0.3) !important;
}

.form-container input {
  width: 100%;
  padding: 10px;
  border: 1px solid #ccc;
  border-radius: 8px;
  font-size: 14px;
  transition: border 0.3s, box-shadow 0.3s;
  font-weight: 400;
  box-sizing: border-box;
}

.form-container input:focus {
  outline: none;
  border-color: #5ab900;
  box-shadow: 0 0 5px rgba(90, 185, 0, 0.5);
}

.form-container button {
  width: 100%;
  padding: 12px;
  border: none;
  border-radius: 8px;
  background: #5ab900;
  color: white;
  font-size: 15px;
  font-weight: bold;
  cursor: pointer;
  transition: background 0.3s;
  margin-top: 10px;
}

.form-container button:hover {
  background: #4aa100;
}

.form-container button:disabled {
  background: #cccccc;
  cursor: not-allowed;
}
</style>