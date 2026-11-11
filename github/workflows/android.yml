
name: Build MKLIONEL APK

on:
  workflow_dispatch:
  push:
    branches: [main]

jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4

      - name: Extract source code
        run: unzip -q MKLIONEL-android-ready-source.zip

      - uses: actions/setup-node@v4
        with:
          node-version: 20

      - name: Install dependencies
        working-directory: mklionel
        run: npm install

      - name: Build website
        working-directory: mklionel
        run: npm run build

      - name: Create Android project
        working-directory: mklionel
        run: npx cap add android

      - name: Sync Android
        working-directory: mklionel
        run: npx cap sync android

      - uses: actions/setup-java@v4
        with:
          distribution: temurin
          java-version: 17

      - name: Build APK
        working-directory: mklionel/android
        run: |
          chmod +x gradlew
          ./gradlew assembleDebug

      - uses: actions/upload-artifact@v4
        with:
          name: MKLIONEL-APK
          path: mklionel/android/app/build/outputs/apk/debug/app-debug.apk
