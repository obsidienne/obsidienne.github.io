---
title: "Simplier les tests avec une fonction forget"
date: 2021-02-25T00:00:00+01:00
slug: "ecto-forget"
tags: [Coding, Elixir]
categories: [TIL]
--- 

Lorsque l'on utilise le scaffold de phoenix, on obtient ce genre de test. Ce sont des tests simples et efficaces.

``` elixir
test "get_comment!/1 returns the comment with given id" do
  comment = comment_fixture()
  assert Reactions.get_comment!(comment.id) == comment
end
```

Le souci, c'est que ça ne va pas fonctionner si vous faites un preload du user dans le context ou si vous utilisez une factory tel que ex_machina

Dans ce genre de cas, il faut créer un mécanisme pour oublier les relations.


``` elixir
defmodule Demp.Repo do
  use Ecto.Repo,
    otp_app: :demo,
    adapter: Ecto.Adapters.Postgres

  def forget(_, _, cardinality \\ :one)

  def forget(struct, fields, cardinality) when is_list(fields)
      fields
      |> Enum.reduce(struct, fn field, acc ->
        forget(acc, field, cardinality)
      end)

  def forget(struct, field, cardinality) do
    %{
      struct
      | field => %Ecto.Association.NotLoaded{
          __field__: field,
          __owner__: struct.__struct__,
          __cardinality__: cardinality
        }
    }
  end
end
```

_Dupliquer de ce [commentaire github](https://github.com/thoughtbot/ex_machina/issues/295#issuecomment-433264227)_