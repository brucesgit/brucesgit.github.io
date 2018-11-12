---
title: JavaScript 中 localStorage 和 sessionStorage 的处理
date: 2018-11-12 17:20:39
tags: 
 - html5
 - javascript
categories: JavaScript
---

```javascript

/**
 * 保存到本地 localStorage
 * @param {String} key 键
 * @param {any} value 值
 * @returns {Boolean} 是否成功
 * @description 保存到本地 localStorage
 */
export const setLocalStorage = (key, value) => {
  // key 值必须为有效字符串，尽管其值的类型不限于 String，但是为了统一，还是规范下。
  if (typeof key !== 'string') {
    return false;
  }
  localStorage.setItem(key, JSON.stringify(value));
  return true;
};

/**
 * 从 localStorage 中取出保存的值
 * @param {String} key 键
 * @returns {any} value 值
 * @description 从 localStorage 中取出保存的值
 */
export const getLocalStorage = key => {
  // key 值必须为有效字符串，尽管其值的类型不限于 String，但是为了统一，还是规范下。
  if (typeof key !== 'string') {
    return;
  }
  const str = localStorage.getItem(key);
  try {
    return JSON.parse(str);
  } catch (error) {
    return str === 'undefined' ? undefined : str;
  }
};

/**
 * 保存到本地 sessionStorage
 * @param {String} key 键
 * @param {any} value 值
 * @returns {Boolean} 是否成功
 * @description 保存到本地 sessionStorage
 */
export const setSessionStorage = (key, value) => {
  // key 值必须为有效字符串，尽管其值的类型不限于 String，但是为了统一，还是规范下。
  if (typeof key !== 'string') {
    return false;
  }
  sessionStorage.setItem(key, JSON.stringify(value));
  return true;
};

/**
 * 从 sessionStorage 中取出保存的值
 * @param {String} key 键
 * @returns {any} value 值
 * @description 从 sessionStorage 中取出保存的值
 */
export const getSessionStorage = key => {
  // key 值必须为有效字符串，尽管其值的类型不限于 String，但是为了统一，还是规范下。
  if (typeof key !== 'string') {
    return;
  }
  const str = sessionStorage.getItem(key);
  try {
    return JSON.parse(str);
  } catch (error) {
    return str === 'undefined' ? undefined : str;
  }
};

```