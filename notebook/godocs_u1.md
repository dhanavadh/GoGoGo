# Miscellaneous in Golang

## underscore in golang
You may see under score in for loop `(_, user)`.

The underscore `_` is Go's way of saying "I don't need this value, so discard it." It's used when a function returns multiple values but you only need some of them.

```go
func getUserByID(c *fiber.Ctx) error {
	id, err := strconv.Atoi(c.Params("id"))
	if err != nil {
		return c.Status(fiber.StatusBadRequest).JSON(fiber.Map{"error": "Invalid user ID"})
	}
	for _, user := range users {
		if user.ID == id {
			return c.JSON(user)
		}
	}
	return c.SendStatus(fiber.StatusNotFound)
}
```

## `range` in Go
When you use range on a slice in Go, it returns two values:

`Index` - the position of the element in the slice (0, 1, 2, etc.)
`Value` - the actual element at that position
In your code:

```go
for _, user := range users {
```

`_` is assigned the index (but you're ignoring it)
`user` is assigned the value (the actual User struct)

If you wanted to use the index, you could write:

```go
for index, user := range users {
    
}
```

But since you only need the User struct itself (not its position in the slice), using _ keeps the code clean and tells other developers that the index isn't needed for this operation.