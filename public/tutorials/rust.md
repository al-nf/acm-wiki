# Rust Tutorial

Written by Alan Fung, 2025.

## Table of Contents
[Rust Tutorial](#rust-tutorial)
- [Table of Contents](#table-of-contents)
- [Introduction](#what-is-rust)
- [Prerequisites](#prerequisites)
- [Installation](#installation)
- [Getting started](#getting-started)

## What is Rust?
Rust is a fast, compiled, type-safe, memory-safe, programming language used in mainly systems and web development. Its unique way of handling memory revolutionizes memory safety, and its package manager and build tool Cargo helps to make development more streamlined. Its similiarity to C and C++ makes it easy to pick up, and it provides advantages such as ease of use and speed.

Rust is a very unique programming language that can teach you a lot and make you more marketable.

## Prerequisites
- 
- Know how to use a computer.

## Installation
The Rust toolchain is installed using `rustup`, and is available on all major platforms.

### Windows
Download and run [rustup-init.exe](https://static.rust-lang.org/rustup/dist/i686-pc-windows-gnu/rustup-init.exe).

### macOS and Linux
Open your terminal, and run the following:\
`curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh`

## Getting started
Create a Rust project with Cargo:\
`cargo new <name>`\
Programs can be compiled and run with `cargo run` or just compiled with `cargo build`. Some useful arguments are listed below:\
`--release`: drastically speeds up performance but leaves out useful debugging features.\
`--bin <binary name>`: compiles a binary stored in src/bin
