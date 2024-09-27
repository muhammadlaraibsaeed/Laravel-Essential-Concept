# Laravel Essentials: Models and Eloquent ORM

## Introduction
This section covers the essential concepts of Eloquent ORM and Models in Laravel, which facilitate the interaction with databases and form the foundation for developing robust web applications.

## Table of Contents
1. [Eloquent ORM](#eloquent-orm)
2. [Creating Models](#creating-models)
3. [Table Naming](#table-naming)
4. [Mass Assignment](#mass-assignment)
5. [Relationships](#relationships)
   - [One-to-One](#one-to-one)
   - [One-to-Many](#one-to-many)
   - [Many-to-Many](#many-to-many)
6. [Query Scopes](#query-scopes)
7. [Eager Loading](#eager-loading)
8. [Accessors and Mutators](#accessors-and-mutators)
   - [Accessors](#accessors)
   - [Mutators](#mutators)
9. [Timestamps](#timestamps)
10. [Soft Deletes](#soft-deletes)
11. [Events](#events)
12. [Database Transactions](#database-transactions)

## Eloquent ORM
- **Definition**: An Active Record implementation for working with databases.
- **Features**: Provides a simple, expressive API for interacting with database tables as models.

## Creating Models
- **Command**: Use `php artisan make:model <ModelName>` to generate a new model.
- **File Location**: Models are typically stored in the `app/Models` directory.

## Table Naming
- **Convention**: Laravel assumes table names are the plural form of the model name (e.g., `Post` corresponds to the `posts` table).

## Mass Assignment
- **Definition**: Allows you to assign multiple attributes to a model at once.
- **Implementation**: Use the `$fillable` property to specify which attributes are mass assignable.

## Relationships
- **One-to-One**: Define relationships between two models (e.g., `User` has one `Profile`).
  - **Method**: 
    ```php
    public function profile() {
        return $this->hasOne(Profile::class);
    }
    ```

- **One-to-Many**: A single model can have multiple related models (e.g., `Post` has many `Comments`).
  - **Method**: 
    ```php
    public function comments() {
        return $this->hasMany(Comment::class);
    }
    ```

- **Many-to-Many**: Define a relationship where both models can have multiple associations (e.g., `User` belongs to many `Roles`).
  - **Method**: 
    ```php
    public function roles() {
        return $this->belongsToMany(Role::class);
    }
    ```

## Query Scopes
- **Definition**: Allows you to define reusable query logic in the model.
- **Implementation**: Use the `scope` prefix in method names (e.g., `scopeActive`).
  - **Example**: 
    ```php
    public function scopeActive($query) {
        return $query->where('active', 1);
    }
    ```

## Eager Loading
- **Definition**: Load relationships alongside the main model to reduce queries.
- **Usage**: Use the `with()` method (e.g., `User::with('posts')->get();`).

## Accessors and Mutators
- **Accessors**: Transform model attributes when accessed.
  - **Implementation**: Define a `get` method (e.g., `getFullNameAttribute()`).
  
- **Mutators**: Modify attributes before saving to the database.
  - **Implementation**: Define a `set` method (e.g., `setPasswordAttribute()`).

## Timestamps
- **Automatic Management**: Eloquent automatically manages `created_at` and `updated_at` timestamps.
- **Disabling Timestamps**: Use the `$timestamps` property set to `false` if not needed.

## Soft Deletes
- **Definition**: Allows for soft deletion of records, meaning they can be restored later.
- **Implementation**: Use the `SoftDeletes` trait.
  - **Example**: 
    ```php
    use Illuminate\Database\Eloquent\SoftDeletes;

    class Post extends Model {
        use SoftDeletes;
    }
    ```

## Events
- **Model Events**: Listen for events like `creating`, `updating`, `deleting`, etc.
- **Implementation**: Use the `static::` method in the model.
  - **Example**: 
    ```php
    protected static function boot() {
        parent::boot();
        static::creating(function ($model) {
            // Logic before creating a model
        });
    }
    ```

## Database Transactions
- **Definition**: Group multiple database operations that either all succeed or all fail.
- **Implementation**: Use the `DB::transaction()` method.
  - **Example**: 
    ```php
    DB::transaction(function () {
        // Multiple database operations
    });
    ```

## Conclusion
Understanding these concepts is crucial for effectively utilizing Eloquent ORM and models in Laravel development.
