package crud

import (
	"gorm.io/gorm"
)

// Crud — базовый CRUD-интерфейс
type Crud[T any] interface {
	Create(entity *T) error
	GetByID(id uint64) (*T, error)
	Get(filter map[string]interface{}) ([]T, error)
	Update(id uint64, entity *T) error
	Delete(id uint64) error
}

// BaseRepo — базовая реализация CRUD
type BaseRepo[T any] struct {
	db *gorm.DB
}

// NewBaseRepo — создаёт новый репозиторий
func NewBaseRepo[T any](db *gorm.DB) *BaseRepo[T] {
	return &BaseRepo[T]{db: db}
}

// Create — создаёт запись
func (r *BaseRepo[T]) Create(entity *T) error {
	return r.db.Create(entity).Error
}

// GetByID — получает запись по ID
func (r *BaseRepo[T]) GetByID(id uint64) (*T, error) {
	var entity T
	err := r.db.First(&entity, id).Error
	return &entity, err
}

// Get — получает записи по фильтру
func (r *BaseRepo[T]) Get(filter map[string]interface{}) ([]T, error) {
	var entities []T
	err := r.db.Where(filter).Find(&entities).Error
	return entities, err
}

// Update — обновляет запись
func (r *BaseRepo[T]) Update(id uint64, entity *T) error {
	return r.db.Model(entity).Where("id = ?", id).Updates(entity).Error
}

// Delete — удаляет запись по ID
func (r *BaseRepo[T]) Delete(id uint64) error {
	return r.db.Delete(new(T), id).Error
}
