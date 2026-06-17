using UnityEngine;

public class BlockStacker : MonoBehaviour
{
    private Rigidbody2D rb;
    private bool isPlaced = false;

    void Start()
    {
        rb = GetComponent<Rigidbody2D>();
    }

    void Update()
    {
        // تحريك القطعة يميناً ويساراً قبل إسقاطها
        if (!isPlaced)
        {
            float move = Mathf.PingPong(Time.time * 2, 4) - 2;
            transform.position = new Vector3(move, transform.position.y, 0);

            if (Input.GetMouseButtonDown(0))
            {
                DropBlock();
            }
        }
    }

    void DropBlock()
    {
        isPlaced = true;
        rb.gravityScale = 1; // تفعيل الجاذبية للسقوط
    }

    void OnCollisionEnter2D(Collision2D collision)
    {
        // عند التصادم نثبت القطعة
        rb.velocity = Vector2.zero;
        rb.angularVelocity = 0;
        
        // هنا يمكنك إضافة منطق "إنشاء قطعة جديدة" بعد فترة قصيرة
    }
}
