using UnityEngine;

public class BearTrap : MonoBehaviour
{
    public float damage = 50f;
    private bool isArmed = true;

    private void OnTriggerEnter(Collider other)
    {
        if (!isArmed) return;

        HunterAI hunter = other.GetComponent<HunterAI>();
        if (hunter != null)
        {
            hunter.TakeDamage(damage);
            isArmed = false;
            Debug.Log("Bot Tuzağa Basarak Hasar Aldı!");
        }
    }
}
using UnityEngine;

public class LootItem : MonoBehaviour
{
    public enum LootType { Ammo, GasMask }
    public LootType type;
    public int ammoAmount = 15;

    private void OnTriggerEnter(Collider other)
    {
        PlayerController player = other.GetComponent<PlayerController>();
        if (player != null)
        {
            if (type == LootType.Ammo)
            {
                player.currentAmmo += ammoAmount;
                Debug.Log(ammoAmount + " Mermi Alındı!");
            }
            else if (type == LootType.GasMask)
            {
                player.EquipGasMask();
            }
            Destroy(gameObject);
        }
    }
}
player.currentAmmo
