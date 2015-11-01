---
layout: post
title: Elixir on Phoenix - OS X Quick Install
---

Here are quick installation instructions to install Elixir and the Phoenix
Framework on OS X. (For the latest, comprehensive installation instructions,
check out the [Phoenix Framework Installation
Docs](http://www.phoenixframework.org/docs/installation).)

### 1. Install Elixir (and Erlang)
Use [Homebrew](http://brew.sh/) to install Elixir.

`brew update`

`brew install elixir`

You may also need to do a `brew link erlang` or a `brew reinstall erlang`.

Elixir compiles down into Erlang for implementation with the Erlang Virtual
Machine.

### 2. Install Hex
Hex is a package manager. You will install Hex with the Mix build tool that
comes with Elixir by running `mix local.hex` on the command line.

### 3. Install Phoenix
Use Mix to install the Phoenix mix archive. The command will look something like
`mix archive.install <path_to_phoenix_mix_archive>`. The [Phoenix installation
docs](http://www.phoenixframework.org/docs/installation#section-phoenix) include
an installation command pointing to the latest stable build.

### 4. Install Node.js
Phoenix uses the npm package ecosystem that comes bundled with
[Node.js](https://nodejs.org/). If you don't already have Node.js installed, I
recommend installing it with [Node Version
Manager](https://github.com/creationix/nvm).

With npm installed, Phoenix will be able to compile static assets using
[brunch.io](http://brunch.io/).

### 5. Install Postgres
The easiest way to get PostgreSQL set up on OS X is with
[Postgres.app](http://postgresapp.com/).

Phoenix looks for a "postgres" user in the database. After installing Postgres,
you can run `psql` from the command line. Then, you will create a new user/role
with login and create permissions by entering `CREATE ROLE postgres LOGIN
CREATEDB;`. (Don't forget the semicolon!) Exit the psql interactive terminal
with Ctrl-D.

### 6. Install Phoenix
(Refer to the [Phoenix Framework Up And Running
Docs](http://www.phoenixframework.org/docs/up-and-running) for the latest,
comprehensive installation instructions.)

Finally, we have all the dependencies we need to install and run Phoenix.
Navigate to the directory where you want to create your Phoenix project
directory then run `mix phoenix.new <application_name>`. e.g. `mix phoenix.new
hello_phoenix`

If prompted, go ahead and fetch and install any dependencies in addition to the Rebar Erlang
build tool. You may need to manually run `mix deps.get` to install
dependencies as well.

After Phoenix successfully installs, navigate to the newly created directory and
run `mix ecto.create`. This will create your Postgres database.

Now, run your application with `mix phoenix.server`. You should then be able to
pull up [http://localhost:4000](http://localhost:4000) in your web browser and
see the Phoenix Framework welcome page.
