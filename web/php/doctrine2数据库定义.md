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
### 整数自增主键
```
    /**
     * @var integer
     *
     * @ORM\Column(type="integer", options={"unsigned"=true})
     * @ORM\Id
     * @ORM\GeneratedValue(strategy="IDENTITY")
     */
    protected $catid;
```

### 字符串类型
```
    /**
     * @var string
     *
     * @ORM\Column
     */
    protected $catid;
```

### 一对一OneToOne
```
    /**
     * @var AdminRole
     * 
     * @ORM\OneToOne(targetEntity="AdminRole",inversedBy="admin_users")
     * @ORM\JoinColumn(name="pid", referencedColumnName="id", onDelete="CASCADE")
     */
    protected $roles;
```

### 多对多ManyToMany
```
    /**
     * @var \Doctrine\Common\Collections\Collection<AdminRole>
     * 
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
     * @var \Doctrine\Common\Collections\Collection<Menu>
     * 
     * @ORM\OneToMany(targetEntity="Deskit\AdminBundle\Entity\Menu", mappedBy="parent")
     */
    protected $children;
```

### 多对一ManyToOne
```
    /**
     * @var Menu
     * 
     * @ORM\ManyToOne(targetEntity="Deskit\AdminBundle\Entity\Menu", inversedBy="children")
     * @ORM\JoinColumn(name="pid", referencedColumnName="id", onDelete="CASCADE")
     */
    protected $parent;
```

### 外键删除规则onDelete
* CASCADE   级联,  主表的行删除,副表的行也删除
* SET NULL  设为空 主表的行删除,副表对应的字段设置为null
* RESTRICT  禁止   只要副表中还有这个主表的这个值,主表就不能删除这一行 默认值

### 在entity做自动添加时间戳
```
 * @ORM\HasLifecycleCallbacks
 */
class Transaction {
```
```
    /** @ORM\PrePersist */
    public function onPrePersist()
    {
        $this->add_time = new \DateTime();
        $this->update_time = new \DateTime();
    }
    /** @ORM\PreUpdate */
    public function onPreUpdate(){
        $this->update_time = new \DateTime();
    }
```