# Auth Bridge для Chrome Extension

Этот репозиторий содержит статические HTML-страницы для редиректов из Supabase в Chrome расширение.

## Установка на GitHub Pages

### Шаг 1: Создайте публичный репозиторий на GitHub

1. Перейдите на [github.com](https://github.com)
2. Создайте новый репозиторий (например, `chrome-extension-auth-bridge`)
3. Убедитесь, что репозиторий **публичный**

### Шаг 2: Загрузите файлы

У вас есть два способа:

#### Вариант А: Через веб-интерфейс GitHub
1. Нажмите "Add file" → "Upload files"
2. Загрузите файлы `confirm.html` и `reset.html`
3. Нажмите "Commit changes"

#### Вариант Б: Через Git (рекомендуется)

```bash
cd /Users/test/Documents/Apps/auth-bridge

# Инициализируем git (если еще не инициализирован)
git init
git add .
git commit -m "Initial commit: Auth bridge pages"

# Добавьте удаленный репозиторий (замените YOUR_USERNAME и REPO_NAME)
git remote add origin https://github.com/YOUR_USERNAME/REPO_NAME.git
git branch -M main
git push -u origin main
```

### Шаг 3: Включите GitHub Pages

1. Перейдите в репозиторий на GitHub
2. Откройте **Settings** → **Pages**
3. Под "Source" выберите **Deploy from a branch**
4. Branch: **main**, folder: **/(root)**
5. Нажмите **Save**

### Шаг 4: Получите URL

Через несколько минут ваш сайт будет доступен по адресу:
```
https://YOUR_USERNAME.github.io/REPO_NAME/
```

Например:
```
https://username.github.io/chrome-extension-auth-bridge/
```

### Шаг 5: Обновите настройки расширения

В файле `src/auth.js` вашего основного проекта обновите URL:

```javascript
// Строка 343-344
const AUTH_BRIDGE_HOST = 'https://YOUR_USERNAME.github.io/chrome-extension-auth-bridge';
const redirectUrl = `${AUTH_BRIDGE_HOST}/reset.html`;

// Строка 642
emailRedirectTo: 'https://YOUR_USERNAME.github.io/chrome-extension-auth-bridge/confirm.html'
```

### Шаг 6: Настройте Supabase

В настройках Supabase Auth → Redirect URLs добавьте:
```
https://YOUR_USERNAME.github.io/chrome-extension-auth-bridge/confirm.html
https://YOUR_USERNAME.github.io/chrome-extension-auth-bridge/reset.html
```

## Структура файлов

- `confirm.html` - страница-мост для подтверждения email
- `reset.html` - страница-мост для сброса пароля

## Безопасность

- ✅ Эти страницы статические и не содержат секретной информации
- ✅ Они только перенаправляют на расширение
- ✅ HTTPS обеспечивается GitHub Pages
- ✅ ID расширения зафиксирован в коде