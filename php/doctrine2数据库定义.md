### entity文件模板
```
use Doctrine\ORM\Mapping as ORM;
/**
 * @ORM\Table(name="deskit_admin_user",uniqueConstraints={@ORM\UniqueConstraint(columns={"user_name"})}  )
 * @ORM\Entity
 */
class AdminUser implements UserInterface{
  ...
}
```
### 一对一OneToOne
```
    /**
     * @ORM\OneToOne(targetEntity="AdminRole",inversedBy="admin_users")
     * @ORM\JoinColumn(name="pid", referencedColumnName="id", onDelete="CASCADE")
     */
    protected $roles;
```

### 多对多ManyToMany
```
    /**
     * @ORM\ManyToMany(targetEntity="AdminRole",inversedBy="admin_users")
     * @ORM\JoinTable(name="deskit_admin_user_role",
     *   joinColumns={@ORM\JoinColumn(name="admin_id", referencedColumnName="id", onDelete="cascade")},
     *   inverseJoinColumns={@ORM\JoinColumn(name="role_id", referencedColumnName="id", onDelete="cascade")}
     * )
     */
    protected $roles;
```


### 一对多OneToMany
```
    /**
     * @ORM\OneToMany(targetEntity="Deskit\AdminBundle\Entity\Menu", mappedBy="parent")
     */
    protected $children;
```

### 多对一ManyToOne
```
    /**
     * @ORM\ManyToOne(targetEntity="Deskit\AdminBundle\Entity\Menu", inversedBy="children")
     * @ORM\JoinColumn(name="pid", referencedColumnName="id", onDelete="CASCADE")
     */
    protected $parent;
```