<script setup lang="ts"></script>

<template>
  <footer>
    <div class="footer_container">
      <div class="date">
        <div class="date_container">
          <FooterDateText text="ПН-ПТ 08:00–19:00; СБ 08:30–14:00">
            <template #icon>
              <Icon name="f7:alarm-fill" />
            </template>
          </FooterDateText>

          <FooterDateText text="Приёмная директора: +7 (8362) 21-56-88">
            <template #icon>
              <Icon name="f7:phone-fill-arrow-down-left" />
            </template>
          </FooterDateText>

          <FooterDateText text="Заместитель директора: +7 (8362) 56-00-80" />

          <FooterDateText text="Вахта: +7 (8362) 21-67-32" />

          <FooterDateText
            text="Марий-Эл, г.Йошкар-Ола, Ленинский проспект, д.10А"
          >
            <template #icon>
              <Icon name="f7:placemark-fill" />
            </template>
          </FooterDateText>
        </div>
      </div>
      <div class="znak">
        <p>© 2025 Школа № 29 имени Героя России Д. Э. Шаймарданова</p>
      </div>
    </div>
  </footer>
</template>

<style scoped lang="scss">
footer {
  min-height: 5rem;
  width: 100%;
  background-color: var(--color-main-page);
  font-weight: 400;
  flex-shrink: 0;
}

.footer_container {
  width: calc(100% - 120px);
  margin-left: auto;
  margin-right: auto;
  max-width: 1000px;
  display: block;
  color: #fff;
  font-size: small;
}

.date {
  padding: 0.5rem;
  margin: auto;
}

.znak {
  width: 100%;
  font-size: smaller;
  display: flex;
  flex-direction: column;
  justify-content: flex-end;
  align-items: center;
  font-weight: 700;
}
</style>
